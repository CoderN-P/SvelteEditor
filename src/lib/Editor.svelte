<script lang="ts">
    import hljs from 'highlight.js';
    import 'highlight.js/styles/default.css';

    export let lines = false;
    export let language = 'typescript';

    let value = "";
    let highlightedText = "";

    function updateValue(event: any) {
        value = event.target.innerText;
        highlightedText = hljs.highlight(value, { language }).value;
    }

    function handleKeydown(event: any) {
        if (event.key === 'Tab') {
            event.preventDefault();
            const textarea = document.getElementById('editor') as HTMLTextAreaElement;
            const start = textarea.selectionStart;
            const end = textarea.selectionEnd;

            console.log(start, end)

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
                value += "\t";
            }
        }
    }

    $: {
        language
        highlightedText = hljs.highlight(value, { language }).value;
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
    <div class="flex flex-row justify-between w-full">
        <div class="flex gap-2 z-50 flex-row">
            <div class="w-3 h-3 rounded-full bg-red-500"></div>
            <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
            <div class="w-3 h-3 rounded-full bg-green-500"></div>
        </div>
        <div class="flex flex-row grow justify-end gap-2">
            <button class="bg-gray-200 hover:bg-gray-300 rounded-md px-2 py-1 text-sm" on:click={() => lines = !lines}>enable line numbers</button>
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
    </div>
</div>
    <div class="flex flex-row mt-4">
        {#if lines}
            <div class="w-6 h-full">
                {#each {length:  value.split(/\r\n|\r|\n/).length === 1 ? 1 : value.split(/\r\n|\r|\n/).length - 1} as _, i}
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
                 data-gramm="false"
                 data-gramm_editor="false"
                 data-enable-grammarly="false"
                    id="editor"
                style="resize: none; white-space: nowrap;"
                class="editor absolute text-transparent px-2 top-0 left-0 mt-0.5 z-50 overflow-x-scroll max-w-full w-full h-full text-sm bg-transparent"
                on:input={updateValue}>
            </div>
            <pre><code class="editor z-0 absolute top-0 left-0 px-2 max-w-full mt-0.5 w-full h-full text-sm bg-transparent">{@html highlightedText}</code></pre>
    </div>

</div>
</div>
