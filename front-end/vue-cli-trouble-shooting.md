Recently, when using vue-cli to create vue project,
the error message

```powershell
vue create [something]
npm ERR! Unexpected end of JSON input while parsing near '[Random Characters]'
```
The problem is caused by unexpected network interruption or anything that produces the wrong cache.

quick solution:

```powershell
npm cache clean --force
```

or

```powershell
npm cache clean --force
npm install
```
