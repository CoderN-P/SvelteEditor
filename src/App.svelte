<script lang="ts">
  import 'highlight.js/styles/atom-one-light.css';
  import Editor from './Editor.svelte';


</script>


<main class="w-full h-screen relative">
    <Editor lines language="python" lineNumberClass="!border-0 bg-gray-900/30 rounded-md" defaultTextClass="text-gray-200/50 text-sm ml-4" caretColor="rgba(255, 255, 255, 0.5)" class="w-3/4 absolute text-gray-200/50 card z-50 !m-8"/>
    <div class="absolute w-52 h-52 z-0 rounded-full m-8 bg-red-500"></div>
</main>

