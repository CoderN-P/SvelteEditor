# SvelteEditor

A simple but customizable code editor made with Svelte and tailwindcss.
(Inspired from [React Simple Code Editor](https://github.com/react-simple-code-editor/react-simple-code-editor/))

## Features

- Syntax highlighting for various languages using highlight.js
- Line numbers
- Customizable styles

## Installation

```bash
npm install -D editor-for-svelte
```
### Make sure you have highlight.js installed for theming

```bash
 npm install -D highlight.js
```


## Usage

### Edit your tailwind.config.js file to add support for the editor

```javascript
/** @type {import('tailwindcss').Config} */
export default {
    content: ["./node_modules/editor-for-svelte/src/**/*.svelte"],
    theme: {
        extend: {},
    },
    plugins: [],
}

```


```svelte

<script>
  import Editor from 'editor-for-svelte';
  import 'highlight.js/styles/github.css'; // Change theme here
</script>

<Editor/>
```

See [examples](#examples) for more

## Props

| Prop            | Type    | Default                                                       | Description                                                                                    | Usage                                       |
|-----------------|---------|---------------------------------------------------------------|------------------------------------------------------------------------------------------------|---------------------------------------------|
| value           | string  | " "                                                           | The code in the editor                                                                         | `<Editor bind:value={code}/>`               |
| language        | string  | "javascript"                                                  | The language of the code (view highlight.js docs for all languages supported)                  | `<Editor language="html"/>`                 |
| lines           | boolean | false                                                         | Show line numbers                                                                              | `<Editor lines/>`                           |
| caretColor      | string  | "black"                                                       | The color of the caret (must be color not class)                                               | `<Editor caretColor="#FFFFFF"/>`            |
| dots            | boolean | false                                                         | Show macOS dots to make it look like a terminal                                                | `<Editor dots/>`                            |
| maxHeight       | string  | "100vh"                                                       | The maximum height of the editor including external padding (recommended to be at least 150px) | `<Editor maxHeight="1000px"/>`              |
| class           | string  | " "                                                           | Additional classes to be added to the editor                                                   | `<Editor class="bg-red-500"/>`              |
| lineNumberClass | string  | " "                                                           | Additional classes to be added to the line number container                                    | `<Editor lineNumberClass="text-gray-400"/>` |
| defaultText     | string  | "Start typing or paste some code to see syntax highlighting!" | The default text to be shown when the editor is empty                                          | `<Editor defaultText="Start typing here"/>` |
| lineSelector    | boolean | false                                                         | Show toggle for line numbers                                                                   | `<Editor lineSelector/>`                    |
| langSelector    | boolean | false                                                         | Show toggle for language                                                                       | `<Editor langSelector/>`                    |
| minHeight       | string  | "80px"                                                        | The minimum height of the editor (including external padding)                                  | `<Editor minHeight="100px"/>`               |
| hljs            | object  | Default hljs object from highlight.js                         | Custom highlight.js object for more customization                                              | `<Editor hljs={customHljs}/>`               |
## Tips

- To change the theme, import the css file from highlight.js and change the theme in the import statement in the script tag
- If a class doesn't apply when adding it as a prop, try placing a `!` before the class to make it important (eg. `!text-red-500`)
- Dont set the height in the class prop, instead use the minHeight and maxHeight props for best results
- If you want multiple editors with different themes, place them in seperate components so that you can import different themes for each editor.
- If you want to use a language that is not included in the default highlight.js package, you can create a custom highlight.js object and pass it as a prop to the editor.

## Examples

```svelte

<script lang="ts">
  import 'highlight.js/styles/github.css';
  import Editor from 'editor-for-svelte';

</script>

<main>
  <div class="w-screen h-screen">
    <Editor class="!rounded-none w-1/2"/>
  </div>
</main>

```

### Output

<img width="575" alt="Screenshot 2024-06-14 at 5 02 37 PM" src="https://github.com/CoderN-P/SvelteEditor/assets/76001641/f58afc1a-a15d-4658-9d04-e75593a3b329">

---


```svelte

<script lang="ts">
  import 'highlight.js/styles/github-dark.css';
  import Editor from 'editor-for-svelte';

  let code = `def hello_world():\n\tprint('Hello, World!')`;
</script>

<main>
  <div class="w-screen h-screen">
    <Editor class="bg-gray-900 text-white w-1/2 !rounded-none" bind:value={code} caretColor="#FFFFFF" lines language="python" lineNumberClass="bg-gray-800 rounded-md !border-0"/>
  </div>
</main>


```

### Output

<img width="572" alt="SvelteEditor example" style="border-radius: 12px;" src="https://github.com/CoderN-P/SvelteEditor/assets/76001641/71e6de77-881f-4240-b3a2-c578dc5320dc">


