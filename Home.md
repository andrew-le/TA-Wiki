**D3** (or **D3.js**) is a JavaScript library for visualizing data using web standards. D3 helps you bring data to life using SVG, Canvas and HTML. D3 combines powerful visualization and interaction techniques with a data-driven approach to DOM manipulation, giving you the full capabilities of modern browsers and the freedom to design the right visual interface for your data.

## Resources

* [Introduction](http://d3js.org/)
* [API Reference](/d3/d3/blob/master/API.md)
* [Release Notes](/d3/d3/blob/master/CHANGES.md)
* [Gallery](/d3/d3/wiki/Gallery)
* [Examples](http://bl.ocks.org/mbostock)
* [Tutorials](/d3/d3/wiki/Tutorials)
* [Plugins](/d3/d3/wiki/Plugins)
* [d3.js on Stack Overflow](http://stackoverflow.com/questions/tagged/d3.js)
* [d3-js Google Group](http://groups.google.com/group/d3-js)
* [d3-js Slack Channel](https://groups.google.com/forum/#!topic/d3-js/vJ3kxaMSkQU%5B1-25%5D)
* [d3-js Gitter Channel](https://gitter.im/d3/d3)
* d3-js IRC Channel => #d3.js on irc.freenode.net

### Translations (Unofficial)

* [한국어](/zziuni/d3/wiki)
* [日本語](/d3/d3/wiki/JP-Home)
* [中文手册](/d3/d3/wiki/API--%E4%B8%AD%E6%96%87%E6%89%8B%E5%86%8C)
* [简体中文](/d3/d3/wiki/CN-Home)
* [繁體中文](/d3/d3/wiki/TW-Home)
* [Русский](/d3/d3/wiki/API-Reference-\(русскоязычная-версия\))
* [Türkçe](/ahmetkurnaz/d3/wiki)
* [Indonesian](/widiantonugroho/d3/wiki)
* [Português](/jeanbauer/d3/wiki)

## Installing

If you use NPM, `npm install d3@next`. Otherwise, download the [latest release](https://npmcdn.com/d3@next/build/). The released bundle supports AMD, CommonJS, and vanilla environments. Create a [custom bundle using Rollup](http://bl.ocks.org/mbostock/bb09af4c39c79cffcde4) or your preferred bundler. You can also load directly from [d3js.org](https://d3js.org):

```html
<script src="https://d3js.org/d3.v4.0.0-alpha.50.js"></script>
```

Or, for the minified version:

```html
<script src="https://d3js.org/d3.v4.0.0-alpha.50.min.js"></script>
```

If you prefer to pin to a specific release, try [CDNJS](https://cdnjs.com/libraries/d3) or [npmcdn](https://npmcdn.com/d3@next/).

## Supported Environments

D3 supports so-called “modern” browsers, which generally means everything _except_ IE8 and older versions. D3 is tested against Firefox, Chrome, Safari, Opera, IE9+, Android and iOS. Parts of D3 may work in older browsers, as the core D3 library has minimal requirements: JavaScript and the [W3C DOM](http://www.w3.org/DOM/) API. D3 uses the [Selectors API](http://www.w3.org/TR/selectors-api/) Level 1, but you can preload [Sizzle](http://sizzlejs.com/) for compatibility. You'll need a modern browser to use [SVG](http://www.w3.org/TR/SVG/) and [CSS3 Transitions](http://www.w3.org/TR/css3-transitions/). D3 is not a compatibility layer, so if your browser doesn't support standards, you're out of luck. Sorry!

D3 also runs on [Node](http://nodejs.org/) and [web workers](http://www.whatwg.org/specs/web-apps/current-work/multipage/workers.html). To use the DOM in Node, you must provide your own DOM implementation; [JSDOM](https://github.com/tmpvar/jsdom) is recommend. To avoid defining a global `document`, pass a DOM element to d3.select or a NodeList to d3.selectAll, like so:

```js
var d3 = require("d3"),
    jsdom = require("jsdom");

var document = jsdom.jsdom(),
    svg = d3.select(document.body).append("svg");
```

## Local Development

Browsers enforce strict security permissions to prevent you from reading files out of the local file system. To develop locally, you must run a local web server rather than using file://…. Node’s [http-server](https://www.npmjs.com/package/http-server) is recommended. To install:

```
npm install -g http-server
```

To run:

```
http-server &
```

This will start the server on <http://localhost:8080> from the current working directory.
