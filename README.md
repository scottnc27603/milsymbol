milsymbol
=========

milsymbol is a small library in pure javascript that creates military unit symbols according to to MIL-STD-2525 and STANAG APP6.

![Figure 13](docs/samples/milsymbol.png?raw=true)

```javascript
new MS.symbol("sfgpewrh--mt", {
	size: 35,
	quantity: 200,
	staffComments: "for reinforcements".toUpperCase(),
	additionalInformation: "added support for JJ".toUpperCase(),
	direction: (750*360/6400),
	type: "machine gun".toUpperCase(),
	dtg: "30140000ZSEP97",
	location: "0900000.0E570306.0N"
}).getMarker().XML;
```

Compared to reference figure from MIL-STD-2525C:


![Figure 13](docs/figure13.png?raw=true)

milsymbol summary
----

milsymbol supports a lot of different options:
 - Both letter and number based SIDC
 - NATO or US standards (MIL-STD-2525C, MIL-STD-2525D, STANAG APP6-(B), STANAG APP6-(D) Draft)
 - Filled/Unfilled symbols
 - Framed/Unframed symbols
 - Text fields
 - Movement indicators
 - SVG/Canvas output (using SVG or Canvas draw instructions)
 - and much more... 
 
For detaild descriptions of what is possible with milsymbol, see the API documentation.


milsymbol can be integrated with most common javascript libraries, such as:
 - Open Layers 3
 - Cesium
 - LeafLet
 - d3
 - Angular
 - and many more...

Examples of some of the integrations are included with milsymbol.

You can find all documentaion and examples at:
http://spatialillusions.com/milsymbol/

Getting started
-----------
You can download [milsymbol from GitHub](https://github.com/spatialillusions/milsymbol "milsymbol"), or install it using npm:
`npm install milsymbol`

To create your first symbol you use the symbol method to create a symbol object:

`MS.symbol(SIDC,{options})`

To make a symbol for an infantry platoon the syntax would be:

`var sym = new MS.symbol("SFG-UCI----D");`

Now `sym` will be a symbol object, but that is not a rendered symbol, this is just information about a symbol, so to create a symbol you use the `getMarker()` method on your symbol object:

`var marker = sym.getMarker();`

And `marker` will now be a symbol object containing information about the size and draw instructions. (For this particular symbol, and in this case `marker` and `sym` will be te same symbol object since `getMarker()` just updates the current object.) 

But you want something to put on your screen, and since milsymbol provides different ways to draw symbol, using SVG or Canvas, you will have to use the method that provides you with the output you want, and for Cesium we want canvas output, so we use `asCanvas()` that returns a canvas element containing the symbol:

`var canvasElement = marker.asCanvas();`

And if you don't want to make it step by step, you can chain it all togheter like this:

`var canvasElement = new MS.symbol("SFG-UCI----D").getMarker().asCanvas();`

![Infantry Platoon](docs/samples/infantry-platoon.png?raw=true)

Options you provided to your symbol can change the size of the symbol, define if it should be filled/unfilled, add text information, and much more; you can read more about all properties and methods in the API documentation provided with milsymbol.

The options can be set when you create your symbol: 

`var sym = new MS.symbol("SFG-UCI----D",{size:35}).getMarker().asCanvas();`

Or they can be updated at any time before you call `getMarker()`:

```
var sym = new MS.symbol("SFG-UCI----D");
sym.size = 35;
var canvasElement = sym.getMarker().asCanvas();
```

When you have requested your symbol using `getMarker()` your symbol object will also contain information about what offset that should be used to get a correct placement, this is stored in the `markerAnchor {x:Number,y:Number}` property.

Technology
----------

milsymbol uses pure javascript to create SVG, Scalable Vector Graphics, and also has built in for native Canvas support. 

 - No external dependencies, just one javascript file required
 - Super fast, can create 1000 symbols in less than 50milliseconds (SVG output)
 
The symbols are created using building blocks defined in the code and no images or fonts are used, this makes it possible to modify almost every aspect of the symbols, such as fill, frame, color, size, stroke width and easily switch between APP6 and 2525 symbology.

To see what is possible with milsymbol use the unit test documents in the docs folder that lists all tabels and figures from the different standards using MilSymbol. (The documents uses milsymbol to render every image that you see, look into the code if you want to see how it is done.)

milsymbol can easily be extended with new functionality and examples of this can be found at: https://github.com/spatialillusions/milsymbol-extensions

Contact
-------
milsymbol is created and maintained by Måns Beckman
 - http://www.spatialillusions.com to see more examples of what milsymbol can be used for
 - https://twitter.com/spatialillusion for milsymbol and mapping/military related information 

Licensing
---------

MIT, See License.txt for details
