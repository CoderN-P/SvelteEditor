<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Editor.svelte'
  import 'highlight.js/styles/github-dark.css';
  import Editor from './lib/Editor.svelte';
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Source+Code+Pro:ital,wght@0,200..900;1,200..900&display=swap" rel="stylesheet">
</svelte:head>

<main>

  <div class="w-screen h-screen overflow-hidden">
    <Editor dots lines class="bg-gray-900 text-white" maxHeight="100vh" caretColor="#FFFFFF" lineNumberClass="border-gray-800 text-gray-400"/>
  </div>

</main>

