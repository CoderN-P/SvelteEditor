<script lang="ts">
    import hljs from 'highlight.js';
    import 'highlight.js/styles/default.css';
    import autosize from 'autosize';

    export let lines = false;
    export let language = 'javascript';
    export let langSelector = false;
    export let dots = false;
    export let lineSelector = false;
    export let value = "";
    export let lineNumberClass = "";
    export let caretColor = "black";
    export let defaultTextClass = "text-gray-400 text-sm ml-2";
    export let maxHeight = "100vh";
    export let defaultText = "Start typing or paste some code to see syntax highlighting!";

    let highlightedText = "";


    function handleKeydown(event: any) {
        if (event.key === 'Tab') {
            event.preventDefault();
            const textarea = document.getElementById('editor') as HTMLTextAreaElement;
            const start = textarea.selectionStart;
            const end = textarea.selectionEnd;

            if (start != end){
                const selectedText = textarea.value.substring(start, end);
                const lines = selectedText.split('\n');

                // Add tab character to each line
                for (let i = 0; i < lines.length; i++) {
                    lines[i] = '\t' + lines[i];
                }

                // Join the lines back together
                const newText = lines.join('\n');

                // Set the new text
                textarea.value = textarea.value.substring(0, start) + newText + textarea.value.substring(end);

                // Update the selection to include the newly indented text
                textarea.selectionStart = start;
                textarea.selectionEnd = start + newText.length;
                value = textarea.value;
            } else {
                document.execCommand('insertText', false, '\t');
            }
        }
    }

    $: {
        highlightedText = hljs.highlight(value, { language }).value;
    }

    $: {
        autosize(document.getElementById('editor'));
        autosize(document.querySelector('pre'));
    }

    function updateScroll(event: any) {
        const textarea = document.getElementById('editor') as HTMLTextAreaElement;
        const pre = document.querySelector('code') as HTMLElement;
        const lines = document.getElementById('lines') as HTMLElement;

        pre.scrollTop = textarea.scrollTop;
        pre.scrollLeft = textarea.scrollLeft;
        if (!lines) return;
        lines.scrollTop = textarea.scrollTop;
    }

</script>
<style>
    .editor {
        align-items: center;
        font-size: 0.875rem/* 14px */!important;
        line-height: 1.25rem/* 20px */!important;
    }

    pre, code {
        font-family: "Source Code Pro", monospace !important;
    }

    .editor:focus {
        outline: none;
    }
    .hide-scrollbar {
        scrollbar-width: none; /* For Firefox */
        -ms-overflow-style: none; /* For Internet Explorer and Edge */
    }

    .hide-scrollbar::-webkit-scrollbar {
        display: none; /* For Chrome, Safari, and Opera */
    }
</style>
<div class="rounded-xl shadow-xl min-h-24 m-4 flex flex-col bg-gray-100 p-4 {$$props.class}" style="max-height: calc({maxHeight} - 32px);">
    <div class="flex flex-row justify-between w-full">
        {#if dots}
            <div class="flex gap-2 z-50 flex-row">
                <div class="w-3 h-3 rounded-full bg-red-500"></div>
                <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                <div class="w-3 h-3 rounded-full bg-green-500"></div>
            </div>
        {/if}
        <div class="flex flex-row flex-1 justify-end gap-2">
            {#if lineSelector}
                <button class="bg-gray-200 hover:bg-gray-300 rounded-md px-2 py-1 text-sm" on:click={() => lines = !lines}>enable line numbers</button>
            {/if}
            {#if langSelector}
                <select class="bg-gray-200 hover:bg-gray-300 rounded-md px-2 py-1 text-sm" bind:value={language}>
                    <option value="typescript">TypeScript</option>
                    <option value="javascript">JavaScript</option>
                    <option value="html">HTML</option>
                    <option value="css">CSS</option>
                    <option value="scss">SCSS</option>
                    <option value="json">JSON</option>
                    <option value="xml">XML</option>
                    <option value="markdown">Markdown</option>
                    <option value="bash">Bash</option>
                    <option value="shell">Shell</option>
                    <option value="yaml">YAML</option>
                    <option value="dockerfile">Dockerfile</option>
                    <option value="plaintext">Plain Text</option>
                </select>
            {/if}
        </div>
    </div>
    <div class="flex flex-row mt-4">
        <div id="lines" class="{lines? 'w-6' : 'w-0'} hide-scrollbar bg-gray-800 overflow-y-hidden" style="max-height: calc({maxHeight} - 96px);">
            {#each {length:  value.split(/\r\n|\r|\n/).length} as _, i}
                <div class="text-gray-400 h-5 pt-0.5 flex items-end relative justify-center px-1 text-sm border-r border-gray-300 {lineNumberClass}">
                    {i + 1}
                </div>
            {/each}
        </div>

        <div class="relative w-full" style="max-height: calc({maxHeight} - 96px);">
            <textarea on:keydown={handleKeydown}
                      spellcheck="false"
                      autocorrect="off"
                      autocapitalize="off"
                      translate="no"
                      data-gramm="false"
                      data-gramm_editor="false"
                      data-enable-grammarly="false"
                      id="editor"
                      on:scroll={updateScroll}
                      style="resize: none; white-space: nowrap;  caret-color: {caretColor};"
                      class="editor absolute text-transparent px-2 top-0 min-h-12 left-0 mt-0.5 z-50 max-h-screen max-w-full w-full h-full text-sm bg-transparent"
                      bind:value={value}/>
            {#if value === ""}
                <div class={defaultTextClass}>
                    {defaultText}
                </div>
            {/if}
            <pre ><code class="editor z-0 absolute top-0 left-0 overflow-x-scroll px-2 max-w-full mt-0.5 w-full min-h-12 max-h-full text-sm bg-transparent">{@html highlightedText}</code></pre>
        </div>

    </div>
</div>
