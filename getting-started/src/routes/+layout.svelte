<script lang="ts">
  import { browser } from '$app/environment'

  import grapesjs, { type Editor, type CommandObject } from 'grapesjs'

  import 'grapesjs/dist/css/grapes.min.css'
  import '../app.css'

  let editor: Editor

  if (browser) {
    editor = grapesjs.init({
      // Indicate where to init the editor. You can also pass an HTMLElement
      container: '#gjs',
      // Get the content for the canvas directly from the element
      // As an alternative we could use: `components: '<h1>Hello World Component!</h1>'`,
      fromElement: true,
      // Size of the editor
      height: '300px',
      width: 'auto',
      mediaCondition: 'max-width', // default is `max-width` -- Desktop-first
      // Avoid HTMLElement default panel
      panels: {
        defaults: [
          {
            id: 'layers',
            el: '.panel__right',
            // Make the panel resizable
            resizable: {
              maxDim: 350,
              minDim: 200,
              tc: false, // Top handler
              cl: true, // Left handler
              cr: false, // Right handler
              bc: false, // Bottom handler
              // Being a flex child we need to change `flex-basis` property
              // instead of the `width` (default)
              keyWidth: 'flex-basis',
            },
          },
          {
            id: 'panel-switcher',
            el: '.panel__switcher',
            buttons: [
              {
                id: 'save-page',
                className: 'fa fa-save',
                command: 'save-page', // Will map to our custom save command
                attributes: { title: 'Save Page' },
              },
              {
                id: 'show-layers',
                active: true,
                label: 'Layers',
                command: 'show-layers',
                // Once activated disable the possibility to turn it off
                togglable: false,
              },
              {
                id: 'show-style',
                active: true,
                label: 'Styles',
                command: 'show-styles',
                togglable: false,
              },
              {
                id: 'show-traits',
                active: true,
                label: 'Traits',
                command: 'show-traits',
                togglable: false,
              },
            ],
          },
          {
            id: 'panel-devices',
            el: '.panel__devices',
            buttons: [
              {
                id: 'device-desktop',
                // label: 'D',
                label:
                  '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M21 14H3V4h18m0-2H3c-1.11 0-2 .89-2 2v12c0 1.1.9 2 2 2h7l-2 3v1h8v-1l-2-3h7c1.1 0 2-.9 2-2V4a2 2 0 0 0-2-2z"></path></svg>',
                command: 'set-device-desktop',
                togglable: false,
              },
              {
                id: 'device-mobile',
                // label: 'M',
                label:
                  '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M16 18H7V4h9m-4.5 18c-.83 0-1.5-.67-1.5-1.5s.67-1.5 1.5-1.5 1.5.67 1.5 1.5-.67 1.5-1.5 1.5m4-21h-8A2.5 2.5 0 0 0 5 3.5v17A2.5 2.5 0 0 0 7.5 23h8a2.5 2.5 0 0 0 2.5-2.5v-17A2.5 2.5 0 0 0 15.5 1z"></path></svg>',
                command: 'set-device-mobile',
                togglable: false,
                active: true,
              },
            ],
          },
        ],
      }, // Disable the storage manager for the moment
      // The Selector Manager allows to assign classes and
      // different states (eg. :hover) on components.
      // Generally, it's used in conjunction with Style Manager
      // but it's not mandatory
      selectorManager: {
        appendTo: '.styles-container',
      },

      styleManager: {
        appendTo: '.styles-container',
        sectors: [
          {
            name: 'Dimension',
            open: false,
            // Use built-in properties
            buildProps: ['width', 'min-height', 'padding'],
            // Use `properties` to define/override single property
            properties: [
              {
                // Type of the input,
                // options: integer | radio | select | color | slider | file | composite | stack
                type: 'integer',
                name: 'The width', // Label for the property
                property: 'width', // CSS property (if buildProps contains it will be extended)
                units: ['px', '%'], // Units, available only for 'integer' types
                defaults: 'auto', // Default value
                min: 0, // Min value, available only for 'integer' types
              },
            ],
          },
          {
            name: 'Extra',
            open: false,
            buildProps: ['background-color', 'box-shadow', 'custom-prop'],
            properties: [
              {
                id: 'custom-prop',
                name: 'Custom Label',
                property: 'font-size',
                type: 'select',
                defaults: '32px',
                // List of options, available only for 'select' and 'radio'  types
                options: [
                  { value: '12px', name: 'Tiny', id: 'tiny' },
                  { value: '18px', name: 'Medium', id: 'medium' },
                  { value: '32px', name: 'Big', id: 'big' },
                ],
              },
            ],
          },
        ],
      },
      layerManager: {
        appendTo: '.layers-container',
      },
      blockManager: {
        appendTo: '#blocks',
        blocks: [
          {
            id: 'section', // id is mandatory
            category: 'Basic',
            // label: '<b>Section</b>', // You can use HTML/SVG inside labels,
            label:
              '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M19 3H5c-1.11 0-2 .89-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5a2 2 0 0 0-2-2m0 2v14H5V5h14z"></path></svg>',
            attributes: { class: 'gjs-block-section' },
            content: `<section>
          <h1>This is a simple title</h1>
          <div>This is just a Lorem text: Lorem ipsum dolor sit amet</div>
        </section>`,
          },
          {
            id: 'text',
            category: 'Basic',
            // label: 'Text',
            label:
              '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M18.5 4l1.16 4.35-.96.26c-.45-.87-.91-1.74-1.44-2.18C16.73 6 16.11 6 15.5 6H13v10.5c0 .5 0 1 .33 1.25.34.25 1 .25 1.67.25v1H9v-1c.67 0 1.33 0 1.67-.25.33-.25.33-.75.33-1.25V6H8.5c-.61 0-1.23 0-1.76.43-.53.44-.99 1.31-1.44 2.18l-.96-.26L5.5 4h13z"></path></svg>',
            content: '<div data-gjs-type="text">Insert your text here</div>',
          },
          {
            id: 'image',
            category: 'Basic',
            // label: 'Image',
            label:
              '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 5c1.1 0 2 .9 2 2v10c0 1.1-.9 2-2 2H4a2 2 0 0 1-2-2V7c0-1.11.89-2 2-2h16M5 16h14l-4.5-6-3.5 4.5-2.5-3L5 16z"></path></svg>',
            // Select the component once it's dropped
            select: true,
            // You can pass components as a JSON instead of a simple HTML string,
            // in this case we also use a defined component type `image`
            content: { type: 'image' },
            // This triggers `active` event on dropped components and the `image`
            // reacts by opening the AssetManager
            activate: true,
          },
        ],
      },
      traitManager: {
        appendTo: '.traits-container',
      },
      deviceManager: {
        devices: [
          {
            name: 'Desktop',
            width: '', // default size
          },
          {
            name: 'Mobile',
            width: '320px', // this value will be used on canvas width
            widthMedia: '480px', // this value will be used in CSS @media
          },
        ],
      },
      storageManager: {
        type: 'local', // Type of the storage, available: 'local' | 'remote'
        autosave: false, // Store data automatically
        autoload: true, // Autoload stored data on init
        stepsBeforeSave: 1, // If autosave enabled, indicates how many changes are necessary before store method is triggered
        options: {
          local: {
            // Options for the `local` type
            key: 'gjsProject', // The key for the local storage
          },
        },
        // ... REMOTE STORAGE CONFIG
        // type: 'remote',
        // stepsBeforeSave: 10,
        // options: {
        //   remote: {
        //     headers: {}, // Custom headers for the remote storage request
        //     urlStore: 'https://your-server/endpoint/store', // Endpoint URL where to store data project
        //     urlLoad: 'https://your-server/endpoint/load', // Endpoint URL where to load data project
        //   },
        // },
      },
      // commands property is a mystery
    })

    // editor.BlockManager.add('my-block-id', {
    //   id: 'my-block-id',
    //   category: 'Ultra',
    //   label: 'my-custom-block',
    //   content: {
    //     tagName: 'div',
    //     draggable: true,
    //     attributes: { 'some-attribute': 'some-value' },
    //     components: [
    //       {
    //         tagName: 'span',
    //         content: '<b>Some static content</b>',
    //       },
    //       {
    //         tagName: 'div',
    //         // use `content` for static strings, `components` string will be parsed
    //         // and transformed in Components
    //         components: '<span>HTML at some point</span>',
    //       },
    //     ],
    //   },
    // })

    editor.Panels.addPanel({
      id: 'panel-top',
      el: '.panel__top',
    })
    editor.Panels.addPanel({
      id: 'basic-actions',
      el: '.panel__basic-actions',
      buttons: [
        {
          id: 'visibility',
          active: true, // active by default
          className: 'btn-toggle-borders',
          // label: '<u>B</u>',
          label:
            '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M15 5h2V3h-2m0 18h2v-2h-2M11 5h2V3h-2m8 2h2V3h-2m0 6h2V7h-2m0 14h2v-2h-2m0-6h2v-2h-2m0 6h2v-2h-2M3 5h2V3H3m0 6h2V7H3m0 6h2v-2H3m0 6h2v-2H3m0 6h2v-2H3m8 2h2v-2h-2m-4 2h2v-2H7M7 5h2V3H7v2z"></path></svg>',
          command: 'sw-visibility', // Built-in command
        },
        {
          id: 'export',
          className: 'btn-open-export',
          // label: 'Exp',
          label:
            '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M5 20h14v-2H5m14-9h-4V3H9v6H5l7 7 7-7z"></path></svg>',
          command: 'export-template',
          context: 'export-template', // For grouping context of buttons from the same panel
        },
        {
          id: 'show-json',
          className: 'btn-show-json',
          // label: 'JSON',
          label:
            '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M8 3c-1.1 0-2 .9-2 2v4c0 1.1-.9 2-2 2H3v2h1c1.1 0 2 .9 2 2v4c0 1.1.9 2 2 2h2v-2H8v-5c0-1.1-.9-2-2-2 1.1 0 2-.9 2-2V5h2V3m6 0c1.1 0 2 .9 2 2v4c0 1.1.9 2 2 2h1v2h-1c-1.1 0-2 .9-2 2v4c0 1.1-.9 2-2 2h-2v-2h2v-5c0-1.1.9-2 2-2-1.1 0-2-.9-2-2V5h-2V3h2z"></path></svg>',
          context: 'show-json',
          command(editor: Editor) {
            editor.Modal.setTitle('Components JSON')
              .setContent(
                `<textarea style="width:100%; height: 250px;">
            ${JSON.stringify(editor.getComponents())}
          </textarea>`,
              )
              .open()
          },
        },
      ],
    })

    // Define commands
    editor.Commands.add('show-layers', {
      getRowEl(editor: Editor) {
        return editor.getContainer()?.closest('.editor-row')
      },
      getLayersEl(row: HTMLElement) {
        return row.querySelector('.layers-container')
      },

      run(editor, sender: HTMLElement) {
        const lmEl = this.getLayersEl(this.getRowEl(editor))
        lmEl.style.display = ''
      },
      stop(editor, sender: HTMLElement) {
        const lmEl = this.getLayersEl(this.getRowEl(editor))
        lmEl.style.display = 'none'
      },
    } as CommandObject)

    editor.Commands.add('show-styles', {
      getRowEl(editor: Editor) {
        return editor.getContainer().closest('.editor-row')
      },
      getStyleEl(row: HTMLElement) {
        return row.querySelector('.styles-container')
      },

      run(editor: Editor, sender: HTMLElement) {
        const smEl = this.getStyleEl(this.getRowEl(editor))
        smEl.style.display = ''
      },
      stop(editor: Editor, sender: HTMLElement) {
        const smEl = this.getStyleEl(this.getRowEl(editor))
        smEl.style.display = 'none'
      },
    } as CommandObject)

    editor.Commands.add('show-traits', {
      getTraitsEl(editor: Editor) {
        const row = editor.getContainer().closest('.editor-row')
        return row.querySelector('.traits-container')
      },
      run(editor: Editor, sender: HTMLElement) {
        this.getTraitsEl(editor).style.display = ''
      },
      stop(editor: Editor, sender: HTMLElement) {
        this.getTraitsEl(editor).style.display = 'none'
      },
    } as CommandObject)

    // Commands
    editor.Commands.add('set-device-desktop', {
      run: (editor) => editor.setDevice('Desktop'),
    })

    editor.Commands.add('set-device-mobile', {
      run: (editor) => editor.setDevice('Mobile'),
    } as CommandObject)

    editor.on('run:export-template', () => console.log('After the command run'))

    editor.on('change:device', () => console.log('Current device: ', editor.getDevice()))
  }

  let { children } = $props()
</script>

{@render children()}
