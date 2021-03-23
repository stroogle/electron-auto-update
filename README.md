## Auto updating electron apps
Modules
```
> yarn add electron electron-builder --dev
> yarn add electron-updater
```
---
package.json
```
"repository":  {
    "type":  "git",
    "url":  "https://github.com/<user>/<your_repo>.git"
},
"scripts":  {
    "start":  "electron .",
    "deploy":  "electron-builder build --mac --win --publish always",
    "build":  "electron-builder build"
}
```
---
electron-builder.yml
```
appId:  com.electron.MyApp
publish:
  provider:  github
win:
  target:  nsis
  verifyUpdateCodeSignature:  false
mac:
  target:  dmg
```
---
main.js
```
// Top of file
const  {  autoUpdater  }  =  require('electron-updater');

// Bottom of file
app.on('ready',  ()  =>  {
    autoUpdater.checkForUpdatesAndNotify();
});
```
**Notes**

This is the most basic form of auto updating and will only work on windows. To do this properly you will need to add listening for events, this will make a better user experience.
```
autoUpdater.on(event, ()=>{
    handleEvent()
})
```
[Check the docs](https://www.electron.build/auto-update#events)