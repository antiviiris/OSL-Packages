# OSL Text Package Documentation

## Methods

```js
text.setProperty( property <str>, value <any>)

text.getProperty( property <str> )
```

Sets and reads the specified property, respectively. More information on properties can be found below.

```js
text.applyStyle( <obj> )
```

Sets multiple properties at once. The argued object is made up of key-value pairs, with the keys being the property to set and the values being what to set it to.

```js
text.resetStyle()
```

Resets all properties to their default configurations.

```js
text.write( text <str> )

text.write( text <str>, width <num>, height <num> )
```

Writes the specified text onto the window, taking into account any properties set using the above methods. A width and height can be specified to aid in alignment and overflow management. Otherwise, the text will automatically determine its width and height.

* * *

## Properties

All properties are stored internally, and normal assignment statements cannot be used to set them. Refer to the above methods on how to configure these properties.  
Properties are very similar to CSS Attributes; they determine how the text is displayed.

| Property | Type | Default Value | Description |
| --- | --- | --- | --- |
| "color" | any | #fff | Determines the color the text is written in. |
| "fontSize" | number | 10  | Determines the size of the text written. |
| "lineSpacing" | number | 1   | Determines how much space is between each line written. Values less than 1 are closer together, while values over 1 multiple the default amount. |
| "align" | "left",  <br>"right",  <br>"center" | "left" | Determines from which direction the text is written. |
| "overflow" | "none",  <br>"trim",  <br>"hidden" | "none" | Determines how the text behaves when it leaves the specified width/height. *None*: the text will keep writing, even if its contents leave the initial area. *Trim*: The text will terminate in an ellipsis (...) if it leaves the specified area. *Hidden*: The text will be surrounded by a frame, causing any excess content to be clipped. |
| "textWrap" | boolean | true | Determines whether the text should automatically insert newlines to stay within the specified width/height. |
| "textFlowX" | \-1 / 0 / 1 | 1   | See below... |
| "textFlowY" | \-1 / 0 / 1 | \-1 | See below... |
| "moveCursor" | boolean | true | When disabled, the draw cursor will revert to its original position after it finishes drawing. |
| "debug" | boolean | false | Intended for development only; inserts a translucent box behind the specified width/height when true. |

## Text Flow

The "textFlowX" and "textFlowY" properties manage how the text is displayed in relation to the draw cursor, and where the draw cursor will end up after being displayed. Both of these values can be set to -1, 0, or 1, representing the direction the cursor will move when rendering. For example, "textFlowX" being set to 1 means that the text will be drawn to the right of the draw cursor, and the draw cursor will end up on the far right side of the text after it's drawn.  

A value being 0 means that that the text will be centered on that axis, and the draw cursor will start and end up in the same x/y position (depending on the variable set). Setting both values to 0 causes the text to render directly on top of the draw cursor, and the cursor will not move after the text is finished rendering.

![A graphic displaying some examples of textFlow in action.](https://raw.githubusercontent.com/antiviiris/OSL-Packages/main/text/doc-assets/textFlow.png)

* * *

## Example Script

```js
body = "https://raw.githubusercontent.com/antiviiris/OSL-Packages/main/text/doc-assets/catgirls.txt".httpGet()

style = {
  "color": "#fff",
  "fontSize": 20,
  "lineSpacing": 1.5,
  "align": "center",
  "textFlowX": 0,
  "textFlowY": -1,
  "overflow": "trim",
  "textWrap": true
}

mainloop:
goto 0 150

text.applyStyle(style)
text.write("What are Cat Girls?")

text.setProperty("fontSize", 10)
text.setProperty("align", "left")
text.write(body, 500, 200)

text.setProperty("align", "right")
text.setProperty("color", "#aaa")
text.write("Written Aug 5th, 2025", 500, 50)

import "win-buttons"
```

![The output for the script above](https://raw.githubusercontent.com/antiviiris/OSL-Packages/main/text/doc-assets/results.png)
