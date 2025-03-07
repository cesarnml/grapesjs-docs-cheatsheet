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

## Sections

- [x] ~~_Introduction_~~ [2025-03-06]
- [x] ~~_Getting Started_~~ [2025-03-06]
- [ ] Modules
  - [ ] Components
  - [ ] Components & JS
  - [ ] Traits
  - [ ] Blocks
  - [ ] Assets
  - [ ] Commands
  - [ ] i18n
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
