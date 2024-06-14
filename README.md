# SvelteEditor

A simple but customizable code editor made with Svelte.
(Inspired from [React Simple Code Editor](https://github.com/react-simple-code-editor/react-simple-code-editor/))

## Features

- Syntax highlighting for various languages using highlight.js
- Line numbers
- Customizable styles

## Installation

```bash
npm install svelte-editor -D
```

## Usage

```svelte

<script>
  import Editor from 'svelte-editor';
</script>

<Editor
  value={code}
  on:input={e => code = e.detail}
  language="javascript"
  style="height: 500px; width: 100%;"
/>
```
