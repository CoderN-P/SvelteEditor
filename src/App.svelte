<script lang="ts">
  import 'highlight.js/styles/github-dark.css';
  import Editor from './Editor.svelte';

  let code = `def hello_world():\n\tprint('Hello, World!')`;
</script>

<main>
  <div class="w-screen h-screen">
    <Editor class="bg-gray-900 text-white w-1/2" bind:value={code} caretColor="#FFFFFF" lines language="python" lineNumberClass="bg-gray-800 rounded-md !border-0"/>
  </div>
</main>

