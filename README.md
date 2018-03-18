
SVG2Bitmap
===========

#### JavaScript SVG to Canvas utility ####

## This project is now dead. ##  

We are sorry, but we don't have time to maintain it, and it started on the wrong path anyway.  
It should have kept itself to only parsing and fetching external assets, instead of trying to do everything from A to Z.

You can still use it, fork it, tweak it freely, but we won't work on it anymore.

Maybe some day it's little sister SVGUnify will finally come to life.

_____

## Old readme ##


The script fixes some issues while drawing SVG on a HTMLcanvas with the built-in [`context.drawImage()`](https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D/drawImage) method.

### How does it work? ###

Most of the svg to canvas libraries does lack of support for external resources (xlink attributes, `<images>`, `<funciri>`, external CSS rules etc.), some svg filters or some other edge cases.
The built-in `drawImage()` method of the [CanvasRenderingContext2D](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D) does an almost perfect rendering of the svg images passed into it.  
The major issue is that external resources won't load into the `<img>` element needed by the `drawImage()` method.  
This script will try to append these resources into the element so they can also be rendered.

### Browser compatibility ###

The script should work fine on the following browsers :

* Firefox 3.5+
* Google Chrome
* Opera 12+
* IE9+ <sup>[1]</sup>
* Safari 6+ <sup>[2]</sup>

<sub>[1]: IE will taint the canvas so no way to get the dataURL version nor to call getImageData() onto the returned canvas.</sub>  
<sub>[2]: Safari 9 does taint the canvas when a `<foreignObject>` is being painted on it.</sub>

### Usage ###

You can call the script like so :  

```javascript    
SVG2Bitmap(sourceElement, [receiver] [, {optionalParameters}]);
```

* **`sourceElement`** can be either an svg node or any HTML Element containing the svg node.
* **`receiver`** can be either a `canvas` element where the svg will be painted, an `<img>` element whose src will be set to the canvas `toDataURL()` result *if available*, a callback function with the canvas and the dataURL *if available* returned as parameters. If `receiver` is not defined, then a callback function replacing the original svg with the canvas copy is executed.

__List of currently available optional parameters :__

*	**`type`** : in which format should be rendered the dataURL() if available. Can be `"image/png"`(default) or `"image/jpeg"`.
*	**`quality`** : if `type` is set to `"image/jpeg"`, this option will set the quality of JPEG compression. (0 to 1 float, 1 being the best)
*	**`scale`** : a positive float to change the rendering size of the element.

__Simple example__  
```javascript
SVG2Bitmap(document.querySelector('svg'), function(canvas, dataURL){
    document.body.appendChild(canvas);
});
```
__Note__

A custom property of the returned canvas named `originalSVG` will keep a link to the original svg node.

### Limitations ###

* Cross-origin resources from an unconfigured server, or on browsers that don't support it will fail to load.  
* Scripts won't execute.
* Only the first frame of SMIL animations will be rendered



### More examples ###

Will never come...