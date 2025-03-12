# GrapesJS Docs Cheatsheet

- [GrapesJS Docs Cheatsheet](#grapesjs-docs-cheatsheet)
  - [Sections](#sections)
  - [Introduction](#introduction)
  - [Getting Started](#getting-started)
    - [Start from the Canvas](#start-from-the-canvas)
    - [Add Blocks](#add-blocks)
    - [Define Components](#define-components)
    - [Panels \& Buttons](#panels--buttons)
    - [Layers](#layers)
    - [Style Manager](#style-manager)
    - [Traits](#traits)
    - [Responsive Templates](#responsive-templates)
    - [Store and Load Data](#store-and-load-data)
    - [Theming](#theming)
  - [Modules](#modules)
    - [Components (Component Manager)](#components-component-manager)
      - [How Components Work?](#how-components-work)
      - [Built-in Components Types (order by priority in `Component Stack`)](#built-in-components-types-order-by-priority-in-component-stack)
      - [Define Custom Component Type](#define-custom-component-type)
      - [Update Component Type](#update-component-type)
      - [Lifecycle Hooks](#lifecycle-hooks)
      - [Components \& CSS](#components--css)
      - [Components \& JS](#components--js)
      - [Tips](#tips)
    - [Components \& JS](#components--js-1)
      - [Basic Scripts](#basic-scripts)
      - [Important Caveat](#important-caveat)
      - [Passing Properties to Scripts](#passing-properties-to-scripts)
      - [Dependencies](#dependencies)
    - [Traits](#traits-1)
      - [Add Traits to Components](#add-traits-to-components)
      - [Built-in Trait Types](#built-in-trait-types)
      - [Updating Traits at Run-time](#updating-traits-at-run-time)
      - [i18N](#i18n)
      - [Customization](#customization)
      - [Events](#events)
    - [Blocks](#blocks)
      - [Configuration](#configuration)
      - [Initialization](#initialization)
      - [Block Content Types](#block-content-types)
      - [Important Caveats](#important-caveats)
      - [Programmatic Usage](#programmatic-usage)
      - [Customization](#customization-1)
      - [Events](#events-1)
    - [Assets (Asset Manager)](#assets-asset-manager)
      - [Basic Configuration](#basic-configuration)
      - [Default Commands](#default-commands)
      - [Stateful Commands](#stateful-commands)
      - [Extending](#extending)
      - [Events](#events-2)
      - [Conclusion](#conclusion)
    - [i18N](#i18n-1)
      - [Configuration](#configuration-1)
      - [Initialization](#initialization-1)
      - [Component-first Selectors](#component-first-selectors)
      - [Programmatic Usage](#programmatic-usage-1)
      - [Customization](#customization-2)
      - [Events](#events-3)
    - [Layers (Layer Manager)](#layers-layer-manager)
      - [Configuration](#configuration-2)
      - [Programmatic Usage](#programmatic-usage-2)
      - [Customization](#customization-3)
      - [Events](#events-4)
    - [Pages](#pages)
      - [Initialization](#initialization-2)
      - [Programmatic Usage](#programmatic-usage-3)
      - [Customization](#customization-4)
      - [Events](#events-5)
    - [Style Manager](#style-manager-1)
      - [Configuration](#configuration-3)
      - [Initialization](#initialization-3)
      - [i18N](#i18n-2)
      - [Component Constraints](#component-constraints)
      - [Programmatic Usage](#programmatic-usage-4)
      - [Customization](#customization-5)
      - [Events](#events-6)
    - [Storage Manager](#storage-manager)
      - [Configuration](#configuration-4)
      - [Project Data](#project-data)
      - [Storage Strategy](#storage-strategy)
      - [Setup Local Storage](#setup-local-storage)
      - [Setup Remote Storage](#setup-remote-storage)
      - [Storage API](#storage-api)
      - [Common Use Cases](#common-use-cases)
      - [Events](#events-7)
    - [Modal](#modal)
      - [Basic Usage](#basic-usage)
      - [Using API](#using-api)
      - [Customization](#customization-6)
      - [Events](#events-8)
    - [Plugins](#plugins)
      - [Basic Plugin](#basic-plugin)
      - [Plugins with Options](#plugins-with-options)
      - [Usage with TS](#usage-with-ts)
      - [Boilerplate](#boilerplate)
  - [Guides](#guides)
    - [Symbols](#symbols)
    - [Replace Rich Text Editor](#replace-rich-text-editor)
    - [Use Custom CSS Parser](#use-custom-css-parser)
    - [GrapesJS Telemetry](#grapesjs-telemetry)

## Sections

- [x] ~~_Introduction_~~ [2025-03-06]
- [x] ~~_Getting Started_~~ [2025-03-06]
- [ ] Modules
  - [ ] _Components_
  - [ ] _Components & JS_
  - [ ] _Traits_
  - [ ] _Blocks_
  - [ ] _Assets_
  - [ ] _Commands_
  - [ ] _i18n_
  - [ ] Selectors
  - [ ] Layers
  - [ ] Pages
  - [ ] Style Manager
  - [ ] Storage Manager
  - [ ] Modal
  - [ ] Plugins
- [ ] Guides
  - [ ] Symbols
  - [ ] Replace Rich Text Editor
  - [ ] Use Custom CSS Parser
  - [ ] GrapesJS Telemetry

## Introduction

- `GrapesJS` is a customizable drag & drop HTML page builder
- Can build for example:
  - [Webpages](https://grapesjs.com/demo.html)
  - [Newsletters](https://grapesjs.com/demo-newsletter-editor.html)
  - [Responsive email templates](https://grapesjs.com/demo-newsletter-editor.html)

## Getting Started

### Start from the Canvas

- The `canvas` is the main part of GrapesJS editor. It's where the **template structure** is defined.

### Add Blocks

- A `block` is a reusable piece of HTML that can be dropped on to the canvas.
  - `Block Manager API` can be used to add blocks dynamically

```js
editor.BlockManager.add("my-block-id", {
  label: "...",
  category: "...",
  // ...
});
```

- A block must have a `id`, `label`, `content` properties

### Define Components

- When a `block` is dragged onto the `canvas` it becomes a `GrapesJS Component`
- A `component` is an `object`
  - managed in the `View`
  - created by the properties in the `Model`
  - All model properties are reflected in the view
- _This section was a bit confusing since it references `Model`, `View` and several `Managers` without much context_

### Panels & Buttons

- `Panels` contain `Buttons` that can execute `actions` (built-in or custom) via a button `command` property

### Layers

- `Layers` provide a tree overview of the HTML structure to facilitate moving around elements

### Style Manager

- `StyleManager` allows adding `class` name attributes and `selector states` to `components` via the `SelectorManager`
- This section is a bit confusing, but basically these two managers are used to construct blocks that enable changing the component default styles and customize active:hover:click states

### Traits

- `Traits` allow for assigning custom attributes and behaviors to components

### Responsive Templates

- Facilitates responsive site checks via programmatic adjustment of the viewport width

### Store and Load Data

- I had difficulty trying to setup the save feature as described in the Getting Started section. There seems to be missing info regarding the `commands` property setup

### Theming

- Via CSS variables or CSS class names

- RECAP: I figured out the styles that work to reproduce the final Get Started setup. However, I haven't figured out how to switch from automatic saving to manually only saves, since that is missing proper documentation. I will need to read through the Storage Manager documentation and possibly delve into the reference API.

## Modules

### Components (Component Manager)

- A `component` is the base element of the template.

#### How Components Work?

- Programmatically add components to the canvas:

```js
// Append components directly to the canvas
editor.addComponents(`<div>
  <img src="https://path/image" />
  <span title="foo">Hello world!!!</span>
</div>`);

// or into some, already defined, component.
// For instance, appending to a selected component would be:
editor.getSelected().append(`<div>...`);

// Actually, editor.addComponents is an alias of...
editor.getWrapper().append(`<div>...`);
```

```js
// surgical programmatic insertion of components
const { length } = component.components();
component.append("<div>...", { at: parseInt(length / 2, 10) });
```

- HTML template strings are parsed into a `Component Definition` (an JSON representation of the component)
- Truncated example of component JSON definition below ... similar to a `Virtual DOM` representation of an `DOM element`:

```js
{
  tagName: 'div',
  components: [
    {
      type: 'image',
      attributes: { src: 'https://path/image' },
    }, {
      tagName: 'span',
      type: 'text',
      attributes: { title: 'foo' },
      components: [{
        type: 'textnode',
        content: 'Hello world!!!'
      }]
    }
  ]
}
```

- Notice that components have an optional `type` property (`Component Type`) that enables the use of built-in/custom components with integrated behaviors
- If omitted, the component has `type: 'default'`
- A component's type is determined via `Component Recognition` which is determined by iterating of the HTML template string by creating the `Component Type Stack` and use of the `isComponent` method
- A `Model` is a `Component` instance

```js
const component = editor.addComponents(`<div>
  <img src="https://path/image" />
  <span title="foo">Hello world!!!</span>
</div>`)[0];
```

```js
const componentType = component.get("type"); // eg. 'image'
```

```js
// Make the component not draggable
component.set("draggable", false);
```

- Notice that the outer wrapping div is not considered a component ... it sorta represent the containing array in some sense

```js
// `.getAttributes` and `.setAttributes` are also methods on a component instance
const innerComponents = component.components();
innerComponents.forEach((comp) => console.log(comp.toHTML())); // logs the innerHTML of a component
// Update component content
component.components(`<div>Component 1</div><div>Component 2</div>`);
```

> The main purpose of the Component is to keep track of its data and to return them when necessary. One common thing you might need to ask from the component is to show its current HTML

- To get back the HTML template string from a component instance: `JSON.stringify(component);`
- A `View` is responsible for rendering a `Component`

```js
const component = editor.getSelected();
// Get the View
const view = component.getView();
// Get the DOM element
const el = component.getEl();
```

> The Model/Component is the source of truth for the final code of templates (eg. the HTML export relies on it) and the View/ComponentView is what is used by the editor to preview our components to users in the canvas.

#### Built-in Components Types (order by priority in `Component Stack`)

- `cell` (opens new window)- Component for handle <td> and <th> elements
- `row` (opens new window)- Component for handle <tr> elements
- `table` (opens new window)- Component for handle <table> elements
- `thead` (opens new window)- Component for handle <thead> elements
- `tbody` (opens new window)- Component for handle <tbody> elements
- `tfoot` (opens new window)- Component for handle <tfoot> elements
- `map` (opens new window)- Component for handle <a> elements
- `link` (opens new window)- Component for handle <a> elements
- `label` (opens new window)- Component for handle properly <label> elements
- `video` (opens new window)- Component for videos
- `image` (opens new window)- Component for images
- `script` (opens new window)- Component for handle <script> elements
- `svg` (opens new window)- Component for handle SVG elements
- `comment` (opens new window)- Component for comments (might be useful for email editors)
- `textnode` (opens new window)- Similar to the textnode in DOM definition, so a text element without a tag element.
- `text` (opens new window)- A simple text component that can be edited inline
- `wrapper` (opens new window)- The canvas need to contain a root component, a wrapper, this component was made to identify it
- `default` (opens new window)Default base component

#### Define Custom Component Type

> The first rule of defining new component types is to place the code inside a plugin.

- Custom Component example:

```js
editor.DomComponents.addType("my-input-type", {
  // Make the editor understand when to bind `my-input-type`
  isComponent: (el) => el.tagName === "INPUT",

  // Model definition
  model: {
    // Default properties
    defaults: {
      tagName: "input",
      draggable: "form, form *", // Can be dropped only inside `form` elements
      droppable: false, // Can't drop other elements inside
      attributes: {
        // Default attributes
        type: "text",
        name: "default-name",
        placeholder: "Insert text here",
      },
      traits: ["name", "placeholder", { type: "checkbox", name: "required" }],
    },
  },
});
```

- Enabling listeners on custom Components Types

```js
editor.DomComponents.addType("my-input-type", {
  // ...
  model: {
    defaults: {
      // ...
      someprop: "initial value",
    },

    init() {
      this.on("change:someprop", this.handlePropChange);
      // Listen to any attribute change
      this.on("change:attributes", this.handleAttrChange);
      // Listen to title attribute change
      this.on("change:attributes:title", this.handleTitleChange);
    },

    handlePropChange() {
      const { someprop } = this.props();
      console.log("New value of someprop: ", someprop);
    },

    handleAttrChange() {
      console.log("Attributes updated: ", this.getAttributes());
    },

    handleTitleChange() {
      console.log("Attribute title updated: ", this.getAttributes().title);
    },
  },
});
```

#### Update Component Type

- Component Model and View can be extended

```js
comps.addType('my-new-component', {
  isComponent: el => {/* ... */},
  extend: 'other-defined-component',
  model: { ... }, // Will extend the model from 'other-defined-component'
  extendView: 'other-defined-component-2',
  view: { ... }, // Will extend the view from 'other-defined-component-2'
});
```

- Model and View listeners can also be extended

```js
domc.addType('new-type', {
  extend: 'parent-type',
  extendFn: ['init'], // array of model functions to extend from `parent-type`
  model: {
    init() {
      // do something
    },
  },
  extendView: 'other-defined-component-2',
  extendFnView: ['init']
  view: {
    init(){
      // do something
    }
  }
});
```

#### Lifecycle Hooks

> Each component triggers different lifecycle hooks, which allows you to add custom actions at their specific stages. We can distinguish 2 different types of hooks: global and local. You define local hooks when you create/extend a component type (usually via some model/view method) and the reason is to react to an event of that particular component type. Instead, the global one, will be called indistinctly on any component (you listen to them via editor.on) and you can make use of them for a more generic use case or also listen to them inside other components.

#### Components & CSS

- Component styles can be added on `model.defaults.styles` property

```js
domc.addType("component-css", {
  model: {
    defaults: {
      attributes: { class: "cmp-css" },
      components: `
        <span>Component with styles<span>
        <div class="cmp-css-a">Component A</div>
        <div class="cmp-css-b">Component B</div>
      `,
      styles: `
        .cmp-css { color: red }
        .cmp-css-a { color: green }
        .cmp-css-b { color: blue }

        @media (max-width: 992px) {
          .cmp-css{ color: darkred; }
          .cmp-css-a { color: darkgreen }
          .cmp-css-b { color: darkblue }
        }
      `,
    },
  },
});
```

- To active Component-First styling behavior

```js
grapesjs.init({
  ...
  selectorManager: {
    componentFirst: true,
  },
})
```

#### Components & JS

- Next section. Delves into Carousel functionality.

#### Tips

### Components & JS

#### Basic Scripts

#### Important Caveat

#### Passing Properties to Scripts

#### Dependencies

### Traits

#### Add Traits to Components

#### Built-in Trait Types

#### Updating Traits at Run-time

#### i18N

#### Customization

#### Events

### Blocks

#### Configuration

#### Initialization

#### Block Content Types

#### Important Caveats

#### Programmatic Usage

#### Customization

#### Events

### Assets (Asset Manager)

#### Basic Configuration

#### Default Commands

#### Stateful Commands

#### Extending

#### Events

#### Conclusion

### i18N

#### Configuration

#### Initialization

#### Component-first Selectors

#### Programmatic Usage

#### Customization

#### Events

### Layers (Layer Manager)

#### Configuration

#### Programmatic Usage

#### Customization

#### Events

### Pages

#### Initialization

#### Programmatic Usage

#### Customization

#### Events

### Style Manager

#### Configuration

#### Initialization

#### i18N

#### Component Constraints

#### Programmatic Usage

#### Customization

#### Events

### Storage Manager

#### Configuration

#### Project Data

#### Storage Strategy

#### Setup Local Storage

#### Setup Remote Storage

#### Storage API

#### Common Use Cases

#### Events

### Modal

#### Basic Usage

#### Using API

#### Customization

#### Events

### Plugins

#### Basic Plugin

#### Plugins with Options

#### Usage with TS

#### Boilerplate

## Guides

### Symbols

### Replace Rich Text Editor

### Use Custom CSS Parser

### GrapesJS Telemetry
