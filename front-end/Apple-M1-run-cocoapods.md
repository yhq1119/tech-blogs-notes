# How to Run pod install on Apple M1 chip machine

1. Go to `/Applications/Utilities` in finder.
2. Right click `Terminal.app` and open menu item `Get Info`.
3. In `General` panel section, check the `Open using Rosetta` box.
4. Completely quit all `Terminal`s and reopen one.
5. Install arm 64 HomeBrew using following command:
   ```shell
   arch -arm64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
6. Add brew command to PATH
Open (or create) the rc file for your shell. Typing echo \$SHELL in your Terminal tells you which shell you’re using. If you’re using Bash, edit \$HOME/.bash_profile or \$HOME/.bashrc. If you’re using Z shell, edit \$HOME/.zshrc. If you’re using a different shell, the file path and filename will be different on your machine.
Add the following line and change [PATH_OF_BREW_DIRECTORY] to be the path of your installation of HomeBrew:
content_copy
 export PATH="\$PATH:[PATH_OF_BREW_DIRECTORY]/bin"
Run source \$HOME/.<rc file> to refresh the current window, or open a new terminal window to automatically source the file.
Verify that the brew/bin directory is now in your PATH by running:
    ```shell
        echo $PATH
    ```
7. Verify that the brew command is available by running:
    ```shell
        which brew
    ```
8. Install arm64 version ruby by using following command:
   ```shell
        arch -arm64 brew install ruby
   ```
   If already installed, you can run:
   ```shell
        arch -arm64 brew reinstall ruby
   ```
9. If you use bash, run following command

    ```shell
    echo 'export PATH=/usr/local/Cellar/ruby/2.4.1_1/bin:$PATH' >> ~/.bash_profile
    ``` 

10. If you use ZSH:
    ```shell
    echo 'export PATH=/usr/local/Cellar/ruby/2.4.1_1/bin:$PATH' >> ~/.zprofile
    ```
11. Install arm64 rbenv
    ```shell
    arch -arm64 brew install rbenv ruby-build
    ```

    if using bash
    ```shell
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
    echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
    ```  

    if using zsh
    ```shell
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zprofile
    echo 'eval "$(rbenv init -)"' >> ~/.zprofile
    ```  

    list all available versions:
    ```shell
    arch -arm64 rbenv install -l
    ```

    install a Ruby version:
    ```shell
    arch -arm64 rbenv install 3.0.1
    ```

    set ruby version for a specific dir
    ```shell
    arch -arm64 rbenv local 3.0.1
    ```

    set ruby version globally
    ```shell
    arch -arm64 rbenv global 3.0.1
    ```

    ```shell
    arch -arm64 rbenv rehash
    arch -arm64 gem update --system
    ```
12. Critial step: Install the ffi library:
    ```shell
    arm64 gem install ffi
    ```

13. Quit `Terminal`, go to `/Applications/Utilities`, Right click `Terminal.app` and open menu item `Get Info`. In `General` panel section, *UNCHECK* the `Open using Rosetta` box.
14. Open `Terminal`, and install cocoapods:
    ```shell
    gem install -n /usr/local/bin cocoapods
    ```
15. Now the pod install should be working properly.
    