**D3** (**Data-Driven Documents** or **D3.js**) is a JavaScript library for visualizing data using web standards. D3 helps you bring data to life using SVG, Canvas and HTML. D3 combines powerful visualization and interaction techniques with a data-driven approach to DOM manipulation, giving you the full capabilities of modern browsers and the freedom to design the right visual interface for your data.    

## Resources

* [Introduction](https://observablehq.com/@d3/learn-d3)
* [API Reference](/d3/d3/blob/main/API.md)
* [Releases](https://github.com/d3/d3/releases)
* [Examples](https://observablehq.com/@d3/gallery)
* [Tutorials](Tutorials)
* [Plugins](Plugins)

### Help & Community

* [Stack Overflow](http://stackoverflow.com/questions/tagged/d3.js)
* [Google Group](http://groups.google.com/group/d3-js)
* [Slack](https://d3js.slack.com) ([Invite](https://d3-slackin.herokuapp.com/))
* [Gitter](https://gitter.im/d3/d3)
* IRC: #d3.js on irc.freenode.net

### Translations (Unofficial)

* [한국어](/zziuni/d3/wiki)
* [日本語](/d3/d3/wiki/JP-Home)
* [中文手册](API--%E4%B8%AD%E6%96%87%E6%89%8B%E5%86%8C)
* [中文手册v4](https://github.com/xswei/d3js_doc)
* [简体中文](CN-Home)
* [繁體中文](TW-Home)
* [Русский](API-Reference-\(русскоязычная-версия\))
* [Türkçe](/ahmetkurnaz/d3/wiki)
* [Indonesian](/widiantonugroho/d3/wiki)
* [Português](/jeanbauer/d3/wiki)
* [Español](/19cah/d3/wiki)

## Getting Started

[Observable](https://observablehq.com/?utm_source=d3js-org&utm_medium=banner&utm_campaign=try-observable) is the quickest way to start playing with D3. Read the [introduction](https://observablehq.com/@d3/learn-d3) or browse the [D3 example gallery](https://observablehq.com/@d3/gallery?utm_source=d3js-org&utm_medium=banner&utm_campaign=try-observable) for inspiration, and then fork a notebook!

## Installing

See https://github.com/d3/d3/blob/main/README.md#installing

## Supported Environments

D3 5+ supports recent browsers, such as Chrome, Edge, Firefox and Safari. D3 4 and below also supports IE 9+. Parts of D3 may work in older browsers, as many D3 modules have minimal requirements. For example, [d3-selection](https://github.com/d3/d3-selection) uses the [Selectors API](http://www.w3.org/TR/selectors-api/) Level 1, but you can preload [Sizzle](http://sizzlejs.com/) for compatibility. You’ll need a modern browser to use [SVG](http://www.w3.org/TR/SVG/) and [CSS3 Transitions](http://www.w3.org/TR/css3-transitions/). D3 is not a compatibility layer, so if your browser doesn’t support standards, you’re out of luck. Sorry!

D3 also runs on [Node](http://nodejs.org/) and [web workers](http://www.whatwg.org/specs/web-apps/current-work/multipage/workers.html). To use the DOM in Node, you must provide your own DOM implementation; [JSDOM](https://github.com/tmpvar/jsdom) is recommended. To avoid defining a global `document`, pass a DOM element to d3.select or a NodeList to d3.selectAll, like so:

```js
import {select} from "d3-selection";
import {JSDOM} from "jsdom";

const jsdom = new JSDOM(html);
const svg = select(jsdom.window.document.body).append("svg");
```

When using D3 in an environment that supports [ES modules](http://exploringjs.com/es6/ch_modules.html), you can import the default D3 bundle as a namespace:

```js
import * as d3 from "d3";
```

If you want to import a D3 module that is not included in the default bundle, you must assign it a separate namespace:

```js
import * as d3 from "d3";
import * as d3GeoProjection from "d3-geo-projection";
```

For this reason, the preferred pattern is to import symbols from the [D3 modules](https://github.com/d3) directly, rather than using the default bundle:

```js
import {select, selectAll} from "d3-selection";
import {geoPath} from "d3-geo";
import {geoPatterson} from "d3-geo-projection";
import "d3-transition";
```

If you are using a bundler, make sure your bundler is configured to consume the `modules` entry point in the package.json. See webpack’s [resolve.mainFields](https://webpack.js.org/configuration/resolve/#resolve-mainfields), for example.

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