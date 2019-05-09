# Building my first Adobe XS plugin  

# Open the plugin development folder 
Plugins > Development > Show Develop Folder menu command, and a new Finder or Explorer window will open, revealing the “develop” folder.  XD expects that you will create a folder for each plugin you want to build. Let’s create a folder for our first plugin. We can name it “my-first-plugin” or just about anything you want (just be sure to name it something you’ll recognize).

# Create your plug-in's manifest 
All XD plugins are required to have a “manifest.” When you save this, make sure the file is named `manifest.json` or your plugin won’t load correctly.

```
{
   "name": "Draw Lots of Rectangles",
   "id": "00000000",
   "version":"1.0.0",
   "description":"Sample plugin for Adobe XD...",
   "icons":[
      {
         "width":96,
         "height":96,
         "path":"images/icon.png"
      }
   ],
   "host":{
      "app":"XD",
      "minVersion":"13.0.0"
   },
   "uiEntryPoints":[
      {
         "type":"menu",
         "label":"Draw lots of rects",
         "commandId":"myPluginCommand"
      }
   ]
}
```
# Input the plugin code
This resides in a file named `main.js`. 

```

const { Rectangle, Color } = require("scenegraph");  // [1]
const commands = require("commands");                // [2]
function myPluginCommand(selection) {                // [3]
  /* all the code we talk about in the next section will 
     go in here */
}
module.exports = {                                   // [4]
  commands: {
    myPluginCommand
  }
};
```

