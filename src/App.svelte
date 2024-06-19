<script lang="ts">
  import 'highlight.js/styles/github-dark.css';
  import Editor from './Editor.svelte';
  import { onMount, onDestroy } from 'svelte';

    let resizeObserver: ResizeObserver | null = null;

  onMount(() => {
      const gradient = document.getElementById('gradient');
      const editor = document.getElementById('mainEditor');

      resizeObserver = new ResizeObserver(entries => {
          for (let entry of entries) {
              if (entry.target === editor) {
                  gradient.style.height = `${editor.clientHeight}px`;
                  gradient.style.width = `${editor.clientWidth}px`;
              }
          }
      });

      resizeObserver.observe(editor);
  });

  onDestroy(() => {
      if (resizeObserver) {
          resizeObserver.disconnect();
      }
  });

</script>


<main class="w-full h-screen flex flex-col overflow-y-scroll items-center p-4 dark:bg-black bg-white">
    <h1 class="font-bold bg-clip-text mt-[20vh] text-8xl text-gray-900 text-transparent bg-gradient-to-r from-orange-500 to-purple-500">Svelte Editor</h1>
    <p class="text-gray-600 dark:text-gray-300">A simple, but customizable code editor for svelte</p>
    <div class="relative w-3/4">
        <Editor id="mainEditor" lines language="python" maxHeight="50vh" lineNumberClass="!border-0 bg-gray-900/30 rounded-md" defaultTextClass="text-gray-200/50 text-sm ml-4" caretColor="rgba(255, 255, 255, 0.5)" class="absolute w-full !ml-0 !top-0 !left-0 text-gray-200/50 bg-gray-900/80 backdrop-blur z-50 !m-8"/>
        <div id="gradient" class="mt-8 h-10 absolute bg-gradient-to-r from-orange-500 to-purple-500 rounded-lg blur-sm w-full z-0"></div>
    </div>
</main>

