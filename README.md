<br>
<img src="https://cdn.jsdelivr.net/gh/nextapps-de/mikado@master/doc/mikado.svg" alt="Mikado.js" width="61.8%">

<h1></h1>
<h3>Web's smartest virtual DOM templating engine. Super-lightweight, outstanding performance, no dependencies.</h3>

<a target="_blank" href="https://www.npmjs.com/package/mikado"><img src="https://img.shields.io/npm/v/mikado.svg"></a>
<a target="_blank" href="https://github.com/nextapps-de/mikado/issues"><img src="https://img.shields.io/github/issues/nextapps-de/mikado.svg"></a>
<a target="_blank" href="https://github.com/nextapps-de/mikado/blob/master/LICENSE"><img src="https://img.shields.io/npm/l/mikado.svg"></a>

<a href="#started">Getting Started</a> &ensp;&bull;&ensp; <a href="#options">Options</a> &ensp;&bull;&ensp; <a href="#api">API</a> &ensp;&bull;&ensp; <a href="#builds">Custom Builds</a>

Demo:

1. <a href="test/demo.html">Standard Javascript</a>
2. <a href="test/demo.es6.html">ES6 Modules</a>

Take a look into the source code of this pages.

Actually in progress:
- Conditional branches
- Includes/partials
- Live Templates (Local Development)

#### Get Latest (Stable Release):

<table>
    <tr></tr>
    <tr>
        <td>Build</td>
        <td>File</td>
        <td>CDN</td>
    </tr>
    <tr>
        <td>mikado.min.js</td>
        <td><a href="https://github.com/nextapps-de/mikado/raw/master/dist/mikado.min.js" target="_blank">Download</a></td>
        <td><a href="https://rawcdn.githack.com/nextapps-de/mikado/master/dist/mikado.min.js" target="_blank">https://rawcdn.githack.com/nextapps-de/mikado/master/dist/mikado.min.js</a></td>
    </tr>
    <tr></tr>
    <tr>
        <td>mikado.light.js</td>
        <td><a href="https://github.com/nextapps-de/mikado/raw/master/dist/mikado.light.js" target="_blank">Download</a></td>
        <td><a href="https://rawcdn.githack.com/nextapps-de/mikado/master/dist/mikado.light.js" target="_blank">https://rawcdn.githack.com/nextapps-de/mikado/master/dist/mikado.light.js</a></td>
    </tr>
    <tr></tr>
    <tr>
        <td>mikado.custom.js</td>
        <td><a href="#builds">Custom Build</a></td>
        <td></td>
    </tr>
</table>


__Node.js__

```npm
npm install mikado
```

__Feature Comparison__
<table>
    <tr></tr>
    <tr>
        <td>Feature</td>
        <td>mikado.min.js</td>
        <td>mikado.light.js</td>
    </tr>
    <tr>
        <td>
            Template Engine
        </td>
        <td>✓</td>
        <td>✓</td>
    </tr>
    <tr></tr>
    <tr>
        <td>
            <a href="#event">Event Binding</a>
        </td>
        <td>✓</td>
        <td>-</td>
    </tr>
    <tr></tr>
    <tr>
        <td>
            <a href="#store">Data Store</a>
        </td>
        <td>✓</td>
        <td>-</td>
    </tr>
    <tr></tr>
    <tr>
        <td>
            <a href="#load">Transport/Load Templates</a>
        </td>
        <td>✓</td>
        <td>-</td>
    </tr>
    <tr></tr>
    <tr>
        <td>
            <a href="#manipulate">DOM Manipulation Collection</a>
        </td>
        <td>✓</td>
        <td>-</td>
    </tr>
    <tr></tr>
    <tr>
        <td>
            <a href="#conditional">Conditional Branches</a>
        </td>
        <td>WIP</td>
        <td>-</td>
    </tr>
    <tr></tr>
    <tr>
        <td>
            <a href="#includes">Includes/Partials</a>
        </td>
        <td>WIP</td>
        <td>-</td>
    </tr>
    <tr>
        <td>File Size (gzip)</td>
        <td>2.1 kb</td>
        <td>1.6 kb</td>
    </tr>
</table>

<a name="api"></a>

## API Overview

Global methods:
- <a href="#mikado.create">Mikado.__new__(template, \<options\>)</a>
- <a href="#mikado.register">Mikado.__register__(template)</a>
- <a href="#mikado.load">Mikado.__load__(url, \<callback\>)</a>

Instance methods:
- <a href="#view.mount">View.__mount__(root)</a>
- <a href="#view.init">View.__init__(template)</a>
- <a href="#view.render">View.__render__(items)</a>
- <a href="#view.create">View.__create__(item)</a>
- <a href="#view.add">View.__add__(item)</a>
- <a href="#view.add">View.__update__(node, item)</a>
- <a href="#view.append">View.__append__(items)</a>
- <a href="#view.clear">View.__clear__()</a>
- <a href="#view.replace">View.__replace__(node, node)</a>
- <a href="#view.sync">View.__sync__()</a>
- <a href="#view.sync">View.__get__(index)</a>
- <a href="#view.sync">View.__index__(node)</a>
- <a href="#view.sync">View.__parse__(template)</a>

Instance methods (not included in mikado.light.js):
- <a href="#view.move">View.__move__(node, index)</a>
- <a href="#view.shift">View.__shift__(node, offset)</a>
- <a href="#view.up">View.__up__(node)</a>
- <a href="#view.down">View.__down__(node)</a>
- <a href="#view.first">View.__first__(node)</a>
- <a href="#view.last">View.__last__(node)</a>
- <a href="#view.before">View.__before__(node, node)</a>
- <a href="#view.after">View.__after__(node, node)</a>
- <a href="#view.swap">View.__swap__(node, node)</a>
- <a href="#view.shuffle">View.__shuffle__()</a>

Instance properties:
- ~~View.__dom__~~
- <a href="#view.length">View.__length__</a>
- <a href="#view.length">View.__store__</a>

<a name="started" id="started"></a>
## Basic Example

Define a HTML-like template and use double curly brackets to mark dynamic expressions which should be calculated during runtime:
```html
<table>
    <tr>
        <td>User:</td>
        <td>{{item.user}}</td>
    </tr>
    <tr>
        <td>Tweets:</td>
        <td>{{item.tweets.length}}</td>
    </tr>
</table>
```

Save this template e.g. to _template/template.html_.

> The preserved keyword ___item___ is a reference to a passed item. You can access the whole nested object.

Install mikado via NPM to make the command line interface available:
```npm
npm install mikado
```

Compile the template through the command line by:
```cmd
mikado template/template.html
```

> __Notation:__ mikado _{{input}} {{destination}}_

Instead of `mikado` you can also use `node task/compile` alternatively. When a destination was not set, the input folder will be used instead.

After compilation you will have 4 different files:
1. __template.js__ the template compiled in ES5 compatible Javascript
2. __template.es6.js__ the template compiled as an ES6 module
3. __template.json__ the template compiled in JSON-compatible notation (<a href="#load">to load via http request</a>)
4. __template.html__ the HTML-like template (reference, do not delete it)

Assume there is an array of data to render (or just one item):
```js
var items = [{
    user: "User A",
    tweets: ["foo", "bar", "foobar"]
},{
    user: "User B",
    tweets: ["foo", "bar", "foobar"]
},{
    user: "User C",
    tweets: ["foo", "bar", "foobar"]
}]
```

Load library and initialize template (ES5):
```html
<script src="mikado.min.js"></script>
<script src="template/template.js"></script>
<script>
    var view = Mikado.new("template");
</script>
```

> The name of a template inherits from its corresponding filename.

Load library and initialize template (ES6):
```html
<script type="module">
    import Mikado from "./mikado.js";
    import template from "./template/template.es6.js";
    var view = Mikado.new(template);
</script>
```

After creation you need mount to a DOM element initially as a destination root and render the template with data:
```js
view.mount(document.body);
view.render(items);
```

You can also chain methods:

```js
var view = Mikado.new(template).mount(document.body).render(items);
```

## Advanced Example

A bit more complex template:
```html
<section id="{{item.id}}" class="{{this.state.theme}}" data-index="{{index}}">
    {{@var is_today = item.date === view.today}}
    <div class="{{item.class}} {{is_today ? 'on' : 'off'}}">
        <div class="title" style="font-size: 2em">{{item.title.toUpperCase()}}</div>
        <div class="content {{index % 2 ? 'odd' : 'even'}}">{{#item.content}}</div>
        <div class="footer">{{view.parseFooter(item)}}</div>
    </div>
</section>
```

You can use any Javascript within the {{ ... }} curly bracket notation.

> To pass html markup as a string, the curly brackets needs to be followed by a "#" e.g. {{#...}}

> To use Javascript outside an elements content you need to prevent concatenation of the returned value. For this purpose the curly brackets needs to be followed by a "@" e.g. {{@...}}

Within a template you have access to the following indentifiers:

<table>
    <tr></tr>
    <tr>
        <td>Identifier</td>
        <td>Description</td>
        <td>Passed Mode</td>
    </tr>
    <tr>
        <td><b>item</b></td>
        <td>A full reference to a passed data item.</td>
        <td>auto</td>
    </tr>
    <tr></tr>
    <tr>
        <td><b>view</b></td>
        <td>An optional payload used to pass non-item specific data or helper functions.</td>
        <td>manual</td>
    </tr>
    <tr></tr>
    <tr>
        <td><b>index</b></td>
        <td>Represents the index of the currently rendered item.</td>
        <td>auto</td>
    </tr>
    <tr></tr>
    <tr>
        <td><b>this</b></td>
        <td>Provides you access to the Mikado view instance.</td>
        <td>auto</td>
    </tr>
    <tr></tr>
    <tr>
        <td>this.<b>state</b></td>
        <td>An object used to keep data as a state across runtime.</td>
        <td>auto (manual set)</td>
    </tr>
    <tr></tr>
    <tr>
        <td>this.<b>store</b></td>
        <td>Gives access to the internal item store (Array).</td>
        <td>auto</td>
    </tr>
    <tr></tr>
    <tr>
        <td>this.<b>length</b></td>
        <td>The length of all items actually rendered (to get length of stored items use <i>this.store.length</i> instead).</td>
        <td>auto</td>
    </tr>
    <tr></tr>
    <tr>
        <td><b>window</b></td>
        <td>The global namespace</td>
        <td>auto</td>
    </tr>
    <tr></tr>
    <tr>
        <td><b>root</b></td>
        <td>Points to the root element of a current rendered template (this is not the root of the view).</td>
        <td>auto</td>
    </tr>
    <tr></tr>
    <tr>
        <td><b>self</b></td>
        <td>Points to the current rendered element itself.</td>
        <td>auto</td>
    </tr>
</table>

You cannot change the naming of those preserved keywords.

It is recommended to pass custom functions via the _view_ object (see example above). You can also nest more complex computations inline as an IIFE and return the result.

```html
<div class="date">{{ 
    (function(){ 
        var date = new Date();
        // ...
        return date.toLocaleString(); 
    }()) 
}}</div>
```

Alternatively of accessing _item_, _view_, _index_ and _this.state_ you can also access variables from the global namespace.

> For performance relevant tasks avoid passing html contents as string.

To finish the example above provide one single or an array of ___item___ data:
```js
var items = [{
    id: "230BA161-675A-2288-3B15-C343DB3A1DFC",
    date: "2019-01-11",
    class: "yellow, green",
    title: "Sed congue, egestas lacinia.",
    content: "<p>Vivamus non lorem <b>vitae</b> odio sagittis amet ante.</p>",
    footer: "Pellentesque tincidunt tempus vehicula."
}]
```

Provide ___view___ data (non-item specific data and helper methods used by the template):
```js
var view = {
    page: 1,
    today: "2019-01-11",
    parseFooter: function(item){ return item.footer; }
}
```

Provide ___state___ data (application specific data and helper methods used by the template):
```js
view.state.theme = "custom";
```

Create a new view instance or initialize a new template factory to an existing instance:
```js
view.init(template);
```

Mount to a new target or just render the already mounted template:
```js
view.render(items, view);
```

Render asynchronously by providing a callback function:
```js
view.render(items, view, function(){
    console.log("finished.");
});
```

To render asynchronously by using promises you need to create the view instance with the ___async___ option flag:
```js
view = Mikado.new(template, { async: true });

view.render(items, view).then(function(){
    console.log("finished.");
});
```

<a name="event" id="event"></a>
## Event Bindings

Lets take this example:
```html
<table data-id="{{item.id}}" root>
    <tr>
        <td>User:</td>
        <td click="show-user">{{item.user}}</td>
        <td><a click="delete-user:root">Delete</a></td>
    </tr>
</table>
```

There are 2 click listeners. The attribute value represents the name of the route. The second listener has a route separated by ":", this will delegate the event from the route "delete-user" to the closest element which contains the attribute "root".

Define routes:
```js
view.route("show-user", function(node){

    alert(node.textContent);

}).route("delete-user", function(node){

    alert(node.dataset.id);
})
```

Routes are stored globally, so you can share routes through all Mikado instances.

<b>List of all supported events:</b>
- change, input, select, toggle
- click, dblclick
- keydown, keypress, keyup
- mousedown, mouseenter, mouseleave, mousemove, mouseout, mouseover, mouseup, mousewheel
- touchstart, touchmove, touchend, touchcancel
- submit, reset
- focus, blur
- load, error
- resize
- scroll

<a name="manipulate" id="manipulate"></a>
## Manipulate Views

You can decide to just one of these:
1. manipulate the DOM directly or
2. use the builtin-methods for those purposes

Using the builtin-methods have the best performance.

> Do not mix manual changes to the DOM with builtin-methods, because manually changes will made the virtual DOM cache out of sync.

Add one item to the end:
```js
view.add(items);
```

Add one item before an index:
```js
view.add(items, 0); // add to beginning
```

Append multiple items to the end:
```js
view.append(items);
```

Append multiple items before an index:
```js
view.append(items, 0); // append to beginning
```

Remove a specific item/node:
```js
view.remove(node);
```

Remove first 20 items:
```js
view.remove(20);
```

Remove last 20 items:
```js
view.remove(-20);
```

Remove all:
```js
view.clear();
```

Replace an item/node:
```js
view.replace(old_node, new_node);
```

Update an single item/node:
```js
view.update(node, item);
```

Move an item/node to a specific index:
```js
view.move(node, 15);
```

Shift an item/node by a specific offset:
```js
view.shift(node, 3);
view.shift(node, -3);
```

Move an item/node to the top or bottom:
```js
view.first(node);
view.last(node);
```

Move an item/node by 1 index:
```js
view.up(node);
view.down(node);
```

Move an item/node before or after another item/node:
```js
view.before(node_a, node_b);
view.after(node_a, node_b);
```

Swap two items/nodes:
```js
view.swap(node_a, node_b);
```

Shuffle items/nodes:
```js
view.shuffle();
```

Get the virtual DOM:
```js
var nodes = view.dom;
```

Re-Sync virtual DOM:
```js
view.sync();
```

<a name="load" id="load"></a>
## Transport / Load Templates

Load template asynchronously into the global cache:
```js
Mikado.load("https://my-site.com/tpl/template.json", function(error){
    if(error){
        console.error(error);
    }
    else{
        console.log("finished.");
    }
});
```

Load template asynchronously with Promises into the global cache:
```js
Mikado.load("https://my-site.com/tpl/template.json", true).then(function(){

    console.log("finished.");

}).catch(function(error){

    console.error(error);
});
```

Load template synchronously by explicit setting the callback to false:
```js
Mikado.load("https://my-site.com/templates/template.json", false);
```

Assign template to a new Mikado instance, mount and render:
```js
var view = Mikado.new("template");
view.mount(document.body).render(items);
```

__.load()__ loads and initialize a new template to an existing Mikado instance:
```js
view.load("https://my-site.com/templates/template.json");
```

__.init()__ assigns a new template to an instance:
```js
view.init("template");
```

__.mount()__ assigns a new root destination to an instance:
```js
view.mount(document.getElementById("new-root"));
```

Chain methods:
```js
view.mount(document.body).init("template").render(items);
```

<a name="includes" id="includes"></a>
## Includes

_WIP_

<a name="conditional" id="conditional"></a>
## Conditional Branches

_WIP_

<a name="builds" id="builds"></a>
## Custom Builds

Perform a full build:
```bash
npm run build
```

Perform a light build:
```bash
npm run build:light
```

Perform a custom Build:
```bash
npm run build:custom ENABLE_CACHE=false LANGUAGE_OUT=ECMASCRIPT5 USE_POLYFILL=true
```

> On custom builds each build flag will be set to _false_ by default.

The custom build will be saved to dist/mikado.custom.xxxxx.js (the "xxxxx" is a hash based on the used build flags).

The destination folder of the build is: _/dist/_

##### Supported Build Flags

<table>
    <tr></tr>
    <tr>
        <td>Flag</td>
        <td>Values</td>
    </tr>
    <tr>
        <td>DEBUG</td>
        <td>true, false</td>
    </tr>
    <tr></tr>
    <tr>
        <td>BUILD_LIGHT</td>
        <td>true, false</td>
    </tr>
    <tr></tr>
    <tr>
        <td>ENABLE_CACHE</td>
        <td>true, false</td>
    </tr>
    <tr>
        <td><br><b>Compiler Flags</b></td>
        <td></td>
    </tr>
    <tr>
        <td>USE_POLYFILL</td>
        <td>true, false</td>
    </tr>
    <tr></tr>
    <tr>
        <td>LANGUAGE_OUT<br><br><br><br><br><br><br><br></td>
        <td>ECMASCRIPT3<br>ECMASCRIPT5<br>ECMASCRIPT5_STRICT<br>ECMASCRIPT6<br>ECMASCRIPT6_STRICT<br>ECMASCRIPT_2015<br>ECMASCRIPT_2017<br>STABLE</td>
    </tr>
</table>

---

Copyright 2019 Nextapps GmbH<br>
Released under the <a href="http://www.apache.org/licenses/LICENSE-2.0.html" target="_blank">Apache 2.0 License</a><br>
