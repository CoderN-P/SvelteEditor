<script lang="ts">
    import hljs from 'highlight.js';
    import 'highlight.js/styles/default.css';

    export let lines = false;
    export let language = 'typescript';

    let value = "";
    let highlightedText = "";


    function updateValue(event: any) {
        value = event.target.innerText;
        if (value.endsWith('\n\n') || value.endsWith('\r\n\r\n') || value.endsWith('\r\r')) {
            value = value.slice(0, -1);
        }

        highlightedText = hljs.highlight(value, { language }).value;
    }

    function handleKeydown(event: any) {
        if (event.key === 'Tab') {
            event.preventDefault();
            document.execCommand('insertText', false, '    ');
            value += '    ';
        }
    }


</script>
<style>
    .editor {
        align-items: center;
        caret-color: black;
        font-size: 0.875rem/* 14px */!important;
        line-height: 1.25rem/* 20px */!important;
    }

    pre, code {
        font-family: "Source Code Pro", monospace !important;
    }

    .editor:focus {
        outline: none;
    }

</style>
<div class="rounded-xl shadow-xl w-3/4 m-4 flex flex-col bg-gray-100 p-4 {$$props.class}">
    <div class="flex gap-2 w-1/2 z-50 flex-row">
        <div class="w-3 h-3 rounded-full bg-red-500"></div>
        <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
        <div class="w-3 h-3 rounded-full bg-green-500"></div>
    </div>
    <div class="flex flex-row mt-4">
        {#if lines}
            <div class="w-6 h-full">
                {#each {length:  value.split(/\r\n|\r|\n/).length} as _, i}
                    <div class="text-gray-400 h-5 pt-0.5 flex items-end relative justify-center px-1 text-sm border-r border-gray-300">
                        {i + 1}
                    </div>
                {/each}
            </div>
        {/if}
        <div class="relative w-full h-52">
            <div on:keydown={handleKeydown}
                spellcheck="false"
                autocorrect="off"
                autocapitalize="off"
                translate="no"
                contenteditable="true"
                style="resize: none;white-space: nowrap;"
                class="editor absolute overflow-x-scroll text-transparent px-2 top-0 left-0 mt-0.5 z-10  max-w-full w-full h-full text-sm bg-transparent"
                on:input={updateValue}>
            </div>
            <pre><code class="editor z-0 absolute overflow-x-scroll top-0 left-0 px-2 max-w-full mt-0.5 w-full h-full text-sm bg-transparent">{@html highlightedText}</code></pre>

    </div>
</div>
</div>
