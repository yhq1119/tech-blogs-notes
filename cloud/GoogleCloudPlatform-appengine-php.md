# Build a simple google php cloud app

### Goal: Build a simple app using appengine & GCP datastore
    - Create login.php, main.php, name.php, password.php
    - Before start the app, add 3 entities into your datastore which has properties like id as key, name as string, password as integer
    - login.php would ask for `id` and `password` to verify if you can login. after login it shoudl redirect to main.php
    - main.php could show the user's name and has two button to redirect to name.php and password.php
    - name.php ask for new name input and if it is empty, it would show error message. If successfully changed, it would redirect to main.php
    - password.php ask for current password and new password, if current password is not correct, it would show error message, if correct, it would redirect to login.php

### Preparation 
## 1. Install Google Cloud SDK (software development kit)
Credit:[Google Offical Documentation](https://cloud.google.com/sdk/docs/downloads-interactive#windows)
  Windows:
  - Download [Installer](https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe)
  Or using command in ***Powershell***
  ```powershell
  (New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", "$env:Temp\GoogleCloudSDKInstaller.exe")

& $env:Temp\GoogleCloudSDKInstaller.exe
  ```
  - Install following instructions
  - Open gcloud shell and type this
  ```powershell
  gcloud init
  ```
  following instructions to setup gcloud i.e. google account, default project
  After finished above steps, you need to
  - learn to use gcloud commands! i.e. 
  ```powershell
  gcloud app deploy
  gcloud app browse
  ```
  
  MacOS:
  Credit:[Quick start for Mac](https://cloud.google.com/sdk/docs/quickstart-macos)
  - Cloud SDK requires Python. Supported versions are 3.5 to 3.7, and 2.7.9 or higher. 
  Modern versions of macOS include the appropriate version of Python required for the Cloud SDK.
  ```unix
  python -V
  ```
  Note: Cloud SDK uses Python 2 by default, but will soon move to Python 3 (run gcloud topic startup for exclusions and more information on configuring your Python interpreter to use a different version). Consider upgrading to Python 3 to avoid disruption in the future.
  - Download one of the following:
  
  |  Platform 	|  Package	 	|  Size 	|  SHA256 Checksum 	|   	|
|---	|---	|---	|---	|---	|
|    macOS 64-bit(x86_64)  	|   [google-cloud-sdk-286.0.0-darwin-x86_64.tar.gz](https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-286.0.0-darwin-x86_64.tar.gz)	|   49.8 MB	|   14a7559466df485b1d42dcc95075efe2ed43f51a6c56a60630dd7209be72036d	|   	|
|  macOS 32-bit(x86) 	|  [google-cloud-sdk-286.0.0-darwin-x86.tar.gz](https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-286.0.0-darwin-x86.tar.gz) 	|  48.8 MB 	|   0955a050d94ff54157e778f1719fa50b6ca67cef106dcf40dbf672c243da1857	|   	|
|   	|   	|   	|   	|   	|

		


		
 - Extract the contents of the file to any location on your file system. If you would like to replace an existing installation, remove the existing ***`google-cloud-sdk`*** directory and extract the archive to the same location.
Optional. Use the install script to add Cloud SDK tools to your path. You'll also be able to opt-in to command-completion for your shell and usage statistics collection. Run the script using this command:
```unix
./google-cloud-sdk/install.sh
```
Open a new terminal so that the changes take effect.

 - Run gcloud init to initialize the SDK:
 ```unix
./google-cloud-sdk/bin/gcloud init
```

## 2. To develop PHP app, we need to install PHP 7
windows:(till 2020-3-28)
- download [this file which is threadsafe](https://windows.php.net/downloads/releases/php-7.4.4-Win32-vc15-x64.zip) or [this file which is NOT threadsafe](https://windows.php.net/downloads/releases/php-7.4.4-nts-Win32-vc15-x64.zip)
- unzip to a directory that you like i.e. ```c:/php74/```
- add the directory path to your system variables (You can find it in system advanced setting)
- test it in powershell by typing this:
```powershell
php -v
```
If you see the information below that means you have done it beautifully.
```
PHP 7.4.4 (cli) (built: Mar 17 2020 12:44:04) ( NTS MSVC15 (Visual C++ 2017) x86 )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.3.8, Copyright (c) 1998-2018 Zend Technologies
```
MacOS:

### Prerequisites
  Before starting the installation of Node.js and NPM using this tutorial you must have the following prerequisites

  - Terminal: You must have Mac Terminal access and little knowledge about working with the terminal application. Ao login to your Mac system and open terminal
  - Homebrew: Homebrew is a popular package manager for the Mac operating systems. It is useful for installing most open source software like Node
.

Download and Install PHP on macOS
The latest version of macOS Sierra ships with PHP 5.6 and similarly OSX 10.11 El Capitan with PHP 5.5, OSX 10.8 Mountain Lion ships with PHP version 5.3. The latest version of PHP 7.2 is available to install. The below steps to help you to install PHP 7.2 or 7.1 or 5.6 on macOS.

Open a terminal and run below commands

***Install PHP 7.3***
```unix
curl -s http://php-osx.liip.ch/install.sh | bash -s 7.3
```
***Install PHP 7.2***
```unix
curl -s http://php-osx.liip.ch/install.sh | bash -s 7.2
```
***Install PHP 7.1***
```unix
curl -s http://php-osx.liip.ch/install.sh | bash -s 7.1
```
***Install PHP 5.6 – Running with OSX 10.11 El Capitan or lower versions.***
```unix
curl -s http://php-osx.liip.ch/install.sh | bash -s 5.6
```
### Verify PHP Installation
The PHP versions for macOS are maintained by php-osx and doesn’t overwrite the current php binaries installed on your system. The installs everything in /usr/local/php5. The new php binary is therefore in /usr/local/php5/bin/php.
```unix
export PATH=/usr/local/php5/bin:$PATH  
```
To verify the correct version of PHP is installed on your system, Execute the following command.
```unix
php -v  
```
```
PHP 7.2.2 (cli) (built: Feb  1 2018 13:23:34) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.2.2, Copyright (c) 1999-2018, by Zend Technologies
    with Xdebug v2.6.0, Copyright (c) 2002-2018, by Derick Rethans
```
Also, create a phpinfo.php under your web root directory with the following contents and access the file in web browser.
```php
<?php phpinfo();?>
```
![phpinfo](https://tecadmin.net/wp-content/uploads/2018/02/php7-macos.png "")


Revert PHP to Default
Don’t you need the latest installed PHP? Simply edit the `/etc/apache2/httpd.conf` and uncomment below the line.

From:
```
LoadModule php5_module /usr/local/php5/libphp5.so
```
to
```
LoadModule php5_module libexec/apache2/libphp5.so
```
And delete the files `+php-osx.conf` and `+entropy-php.conf` from `/etc/apache2/other directory`.

## 3. Do NOT forget the PHP package manager composer!
Credit: [Composer Installation Document](https://getcomposer.org/download/)
install on windows:
- download [this installer](https://getcomposer.org/Composer-Setup.exe) and run it!
install on MacOS:
- open terminal and typing this below:
```unix
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```
for convenience, I'd like to install globally, so...type this command
```unix
mv composer.phar /usr/local/bin/composer
```
Alternatively, if you have the installer for mac unix linux and want to install locally, go to the folder in terminal and:
```unix
php composer-setup.php --install-dir=bin --filename=composer
```

### Development (Windows using Visual Studio Code)
- create your folder 
```powershell
mkdir php-gcp-app
cd php-gcp-app
```
- create ~/app.yaml (if you want to use some css file at /css folder, create it in your project folder and add it in the yaml file like this:)
```yaml
runtime: php7
api_version: 1

handlers:
 - url: /
   script: index.php
 - url: /css
   static_dir: css
```
- install google/cloud/datastore (notice: this should be in the folder which has composer.json)
```powershell
composer require google/cloud-datastore
```

## Core function of GCP datastore (Create Read Update Delete)
- Prerequisites
  ```php
  <?php
  require 'vendor/autoload.php';
  use Google\Cloud\Datastore\DatastoreClient;
  $datastore = new DatastoreClient([
      'projectId'=>'/*YOUR PROJECT ID*/'
  ]);
  ?>
  ``
- Create
  two ways and I prefer second
  
  One:
  ```PHP
  <?php
  $task = $datastore->entity('/YOUR KIND NAME/',[
    'id'=>'YOUR ID',
    'name'=>'YOUR NAME',
    'password'=>'YOUR PASSWORD'
  ]);
  $datastore->insert($task);
  ?>
  ```
  Two:
  ```PHP
  <?php
  $key = $datastore->key('/YOUR KIND NAME/','/KEY SET BY YOU/');
  $task = $datastore->entity($key,[
     'id'=>'YOUR ID',
     'name'=>'YOUR NAME',
     'password'=>'YOUR PASSWORD'
  ]);
  $datastore->upsert($task);
  ?>
  ```
  
- Read(lookup)
  Notice, here suggests the person has known the key
  ```PHP
  <?php
    $key = $datastore->key('/YOUR KIND NAME/','/KEY THAT YOU KNOW/');
    $task = $datastore->lookup($key);
  ?>
  ```
- Update
  Notice, here suggests the person has known the key
  ```PHP
  <?php
    $key = $datastore->key('/YOUR KIND NAME/','/KEY THAT YOU KNOW/');
    $task = $datastore->lookup($key);
    $task['/THE PROPERTY YOU WANT TO EDIT/']='/THE VALUE YOU EDIT/';
    $datastore->update($task);
  ?>
  ```
  
- Delete
  ```PHP
  <?php
    $key = $datastore->key('/YOUR KIND NAME/','/KEY THAT YOU KNOW/');
    $datastore->delete($key);
  ?>
  ```
  
  ## Core functions of PHP 
  - redirecting
  ***NOTICE***
  ***The php script that contains header() method should be on the top of the file, which means the start of the file is the start of the php script without blank line***
  ```PHP
  <?php
  header('Location: /URL THAT YOU WANT TO GO/');
  exit;
  ?>
  <!DOCTYPE html>
  <html>
    ...
  </html>
  ```
  - store and retrieve data from $_SESSION
  ```PHP
  <?php
  session_start();
  // store
  $_SESSION['/KEY YOU WANT TO USE/']='/VALUE YOU WANT TO STORE/';
  // retreive
  $variable = $_SESSION['/KEY YOU KNOW/'] // now the $variable has the value
  ?>
  ```
  - trigger the function by POST method
  ```PHP
  <?php
  if(isset($_POST['/KEY YOU WANT TO USE/'])){// this check if $_POST has the key
  // do what you want to
  }
  // OR
  if(array_key_exists('/KEY YOU WANT TO USE/',$_POST)){// similar as above
  // do whatever
  }
  // OR
  if ($_SERVER['REQUEST_METHOD'] == 'POST'){// this checks if there is a post request
  // do whatever
  }
  // OR
  if($_POST){// this checks if there is A POST REQUEST THAT HAS DATA
  // do whatever
  }
  ?>
  <!DOCTYPE html>
  <html>
    <body>
      <form action='',method='post'>
        <input name='/KEY YOU WANT TO USE/' type='submit'>  
      </form>
    </body>
  </html>
  ```
  <s>Maybe you can also do this to $_GET</s>
  - echo!
  ```PHP
  if($flag){
     echo "<span style='color: red'>Error Message</span>"
  }
  ```


## Sometimes the datastore would need to create index for its instances.
   To solve that you can simply deploy the index.yaml
     ```Powershell
 gcloud app deploy index.yaml --project=/YOUR PROJECT ID/
  ```
  
 # Now we have all the needed knowledge to build it. Let's make a simplest one!
 

