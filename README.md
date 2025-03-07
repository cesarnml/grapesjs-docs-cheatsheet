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
      - [Built-in Components Types](#built-in-components-types)
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

- RECAP: I figured out the styles that work to reproduce the final Get Started setup. However, I haven't figured out how to switch from automatic saving to manually only saves, since that is missing proper documentation. I will need to read through the Storage Manager documentation and possibly delve into the reference API.

## Modules

### Components (Component Manager)

- A `component` is the base element of the template.

#### How Components Work?

#### Built-in Components Types

#### Define Custom Component Type

#### Update Component Type

#### Lifecycle Hooks

#### Components & CSS

#### Components & JS

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
