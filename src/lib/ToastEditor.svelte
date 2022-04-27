<script>
	// import Editor from '@toast-ui/editor';
	import '@toast-ui/editor/dist/toastui-editor.css';
	import { onMount } from 'svelte';

	export let htmlOutput = '';
	export let height = '400px';
	export let code = false;
	let editor;
	let element;

	onMount(async () => {
		const EditorImport = await import('@toast-ui/editor');
		console.log(EditorImport);
		const Editor = EditorImport.default;
		editor = new Editor({
			el: element,
			events: { change: handleChange },
			initialEditType: 'wysiwyg',
			usageStatistics: false,
			hideModeSwitch: true,
			initialValue: htmlOutput,
			height: height
		});
		if (!code) {
			editor.removeToolbarItem('code');
			editor.removeToolbarItem('codeblock');
		}
	});

	// const createEditor = (node) => {

	// };

	const handleChange = () => {
		htmlOutput = editor.getHTML();
	};
</script>

<div id="editor" bind:this={element} />

<style>
</style>
