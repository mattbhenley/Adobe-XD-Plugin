# Building my first Adobe Xd plugin 

We'll be building a plugin called "Draw Lots of Rectangles"

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

# Implement the plugin logic

```

const rect = new Rectangle();
rect.width = 320;
rect.height = 320;
```

```

rect.fill = null;
rect.stroke = new Color("white");
rect.opacity = 0.5;
```

# Add the rectangle to the canvas

`selection.insertionParent.addChild(rect);`

# Select the rectangle 

`selection.items = [rect];`

# Duplicate the selection 

`commands.duplicate();`

# Rotate it 

```

const node = selection.items[0]; 
node.rotateAround(5, node.localCenterPoint);
```

# Move it 

`node.moveInParentCoordinates(5, 0);`

# Repeat

```

let times = 0;
while (times < 179) {
  // steps 6 - 9
  commands.duplicate();
  const node = selection.items[0];
  node.rotateAround(5, node.localCenterPoint);
  node.moveInParentCoordinates(5, 0);
  // end of steps 6 - 9
  
  times += 1;
}
```

# Finished Plugin 

![RectanglesPlugin](https://github.com/mattbhenley/Images/blob/master/spirals.png)