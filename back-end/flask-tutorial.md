### Funny

Credit: https://flask.palletsprojects.com/en/1.1.x/

###### Simple install
```powershell
pip install Flask
```
###### Minimal App
***create your folder***
```powershell
mkdir yourflask
cd yourflask
```
***create your app.py inside the folder***
```powershell
nano app.py
```
***write your first code!***
```Python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```
***Run it and see***
```powershell
python app.py
```
