<script lang="ts">
	import { browser, building, dev, version } from '$app/environment';

	import grapesjs, { type Editor } from 'grapesjs';

	import 'grapesjs/dist/css/grapes.min.css';
	import '../app.css';

	let editor: Editor;

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
			// Disable the storage manager for the moment
			storageManager: false,
			// Avoid any default panel
			panels: { defaults: [] }
		});
		console.log(editor.getConfig());
	}

	let { children } = $props();
</script>

{@render children()}
