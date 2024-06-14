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
  import 'highlight.js/styles/atom-one-dark.css'; // Change theme here
  
  
</script>

<Editor/>
```


## Props

| Prop            | Type    | Default      | Description                                                                   | Usage                                       |
|-----------------|---------|--------------|-------------------------------------------------------------------------------|---------------------------------------------|
| value           | string  | " "          | The code in the editor                                                        | `<Editor bind:value={code}/>`               |
| language        | string  | 'javascript' | The language of the code (view highlight.js docs for all languages supported) | `<Editor language="html"/>`                 |
| lines           | boolean | false        | Show line numbers                                                             | `<Editor lines/>`                           |
| caretColor      | string  | 'black'      | The color of the caret (must be color not class)                              | `<Editor caretColor="#FFFFFF"/>`            |
| dots            | boolean | false        | Show macOS dots to make it look like a terminal                               | `<Editor dots/>`                            |
| maxHeight       | string  | '100vh'      | The maximum height of the editor (including external padding)                 | `<Editor maxHeight="1000px"/>`              |
| class           | string  | ''           | Additional classes to be added to the editor                                  | `<Editor class="bg-red-500"/>`              |
| lineNumberClass | string  | ''           | Additional classes to be added to the line number container                   | `<Editor lineNumberClass="text-gray-400"/>` |
| defaultText     | string  | ''           | The default text to be shown when the editor is empty                         | `<Editor defaultText="Start typing here"/>` |
| lineSelector    | boolean | false        | Show toggle for line numbers                                                  | `<Editor lineSelector/>`                    |
| langSelector    | boolean | false        | Show toggle for language                                                      | `<Editor langSelector/>`                    |