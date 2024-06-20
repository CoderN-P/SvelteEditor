<script lang="ts">
  import 'highlight.js/styles/tokyo-night-dark.css';
  import Editor from './Editor.svelte';
  import { onMount, onDestroy } from 'svelte';

  let resizeObserver: ResizeObserver | null = null;

  onMount(() => {
      const gradient = document.getElementById('gradient');
      const editor = document.getElementById('mainEditor');

      if (!editor || !gradient) {
          return;
      }

      function outputsize() {
          if (editor && gradient) {
              gradient.style.height = `${editor.clientHeight}px`;
          }
      }

      outputsize();

    resizeObserver = new ResizeObserver(outputsize);
    resizeObserver.observe(editor);

  });

  onDestroy(() => {
      if (resizeObserver) {
          resizeObserver.disconnect();
      }
  });

  let code = "npm install editor-for-svelte";

</script>

<style>
    main {
        scrollbar-width: none; /* For Firefox */
        -ms-overflow-style: none; /* For Internet Explorer and Edge */
    }

    main::-webkit-scrollbar {
        display: none; /* For Chrome, Safari, and Opera */
    }
</style>


<main class="w-full h-full flex flex-col dark:bg-black bg-white">
    <div class="w-full h-screen flex items-center flex-col p-4">
        <div class="absolute top-0 p-4 flex flex-row justify-between left-0 w-screen bg-gray-950/50 border-b border-gray-800 backdrop-blur h-20">
            <div class="flex flex-row gap-4 items-center">
                <a href="https://neelp.tech"><img src="https://neelp.tech/static/images/codern_pfp.gif" alt="Neel Parpia" class="hover:opacity-80 w-10 h-10 rounded-full"></a>
                <p class="font-semibold text-white">Made by Neel Parpia</p>
            </div>
            <div class="flex flex-row gap-4 items-center">
                <a href="https://github.com/CoderN-P/SvelteEditor"><img src="/github-mark-white.svg" alt="GitHub" class="w-8 h-8 hover:opacity-80 cursor-pointer"></a>
                <a href="https://npmjs.com/package/editor-for-svelte"><img src="/npm-icon.svg" alt="GitHub" class="w-8 h-8 hover:opacity-80 rounded-md cursor-pointer"></a>
            </div>
        </div>
        <h1 class="font-bold bg-clip-text mt-[20vh] text-6xl text-gray-900 text-transparent bg-gradient-to-r from-orange-500 to-purple-500">Svelte Editor</h1>
        <p class="text-gray-600 mt-2 dark:text-gray-400">A <strong>simple</strong>, but <strong>customizable</strong> code editor for svelte</p>
        <div class="relative mt-[5vh] w-3/4">
            <Editor id="mainEditor" lines langSelector lineSelector bind:value={code} lineSelectorClass="bg-gray-900/50 hover:bg-gray-900/60" dots langSelectorClass="bg-gray-900/50 hover:bg-gray-900/60" language="shell" maxHeight="40vh" lineNumberClass="!border-0 bg-gray-900/30 rounded-md" defaultTextClass="text-gray-200/50 text-sm ml-4" caretColor="rgba(255, 255, 255, 0.5)" class="absolute w-full !ml-0 !top-0 !left-0 text-gray-200/50 bg-gray-950 backdrop-blur z-50 !m-8"/>
            <div id="gradient" class="mt-8 h-10 absolute bg-gradient-to-r from-orange-500 to-purple-500 rounded-lg blur-sm w-full z-0"></div>
        </div>
    </div>
</main>

