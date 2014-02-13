# kolor

*kolor* is a useful color manipulation tool in JavaScript.

It provides color string parsing, format converting and basic color adjusting methods.

Supported color formats:

*   RGB(A)
*   HSL(A)
*   HSV(A)


## Usage

* [Vanilla JS](http://vanilla-js.com/)

    Just include `kolor.js` in your HTML document:

        <script src="kolor.js"></script>

    Core functionalities are provided by the `kolor` object in global scope.

* Working with [RequireJS](http://requirejs.org/) (or other AMD compatible loaders)

    Just require the named module `kolor`:

        require(['kolor'], function(kolor) {
            // Starts here
        });

* Working with [npm](https://npmjs.org/)

        npm install kolor


### Creating a color object

Colors may be created in the following ways:

1.  By parsing a given string value

        var red = kolor('red'), //color name
            green = kolor('rgb(0, 255, 0)'), //valid CSS expressions
            blue = kolor('rgba(0%, 0%, 100%, 1)'), //more valid CSS expressions
            cyan = kolor('hsv(180, 1, 1)'), //not supported by CSS but has a similar syntax
            magenta = kolor('#ff00ff'), //hex RGB value
            yellow = kolor('ff00ff'); //hex RGB value without '#'

    Color names are defined by [W3C SVG color names used in CSS3](http://www.w3.org/TR/css3-color/#svg-color).

    Names or hex values will generate RGB colors.

2.  By specifying a color format

        var red = kolor.rgb(255, 0, '0%'), //can use either number or percent string
            green = kolor.rgb([0, 255, 0]), //using array
            blue = kolor.rgb({ r: 0, g: 0, b: 255 }); //using object

3.  By cloning another color object

        var red = kolor('red'),
            newRed = kolor(red);

*Created colors are in certain formats and can be converted to other formats.*

### Accessors

*kolor* provides jQuery-like accessors for color objects.

    color.red(128); //altering 'red' channel
    color.r(255); //shorthand method is also available

    console.log(color.r()); //255

Setters return color object itself so we can do a bit of chaining:

    color.r(255).g(128).b(128); //making it lighter

### Value restriction

When setting a value of a channel, the specified value will be automatically restricted within a valid range according to the channel configuration.

    console.log(rgbColor.r(300).r()); //255
    console.log(hslColor.h(-10).h()); //350
    console.log(hsvColor.s('200%').s()); //1

### Format conversion

Once a color object is created, it can be easily converted to other formats. After each conversion, a new color object will be produced and returned.

    var hsvColor = rgbColor.hsv().h(120); //converts and sets

### String output

    console.log(red.hex()); //'#ff0000'
    console.log(red.css()); //'rgb(255, 0, 0)'

### Color modification

A color can be modified into another in many ways. After each modification, a new color object is produced and returned.

    color = red.spin(180); //spins the color wheel for 180 degrees
    color = red.mix(blue, 0.3); //mixes two colors with a given proportion.
    color = red.lighten(0.2); //gets a lighter color


For full features and API documentation, please read [this documentation](http://justineo.github.com/kolor/docs/) generated by [Docco](http://jashkenas.github.com/docco/).
