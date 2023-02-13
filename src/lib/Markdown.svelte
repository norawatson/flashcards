<script lang="ts">
  import { Editor, rootCtx, defaultValueCtx, editorViewOptionsCtx } from '@milkdown/core';
  import { replaceAll } from '@milkdown/utils';
  import { commonmark } from '@milkdown/preset-commonmark';
  import { gfm } from '@milkdown/preset-gfm';
  import { math } from '@milkdown/plugin-math';
  import { clipboard } from '@milkdown/plugin-clipboard';
  import { upload } from '@milkdown/plugin-upload';
  import { history } from '@milkdown/plugin-history';
  import { listener, listenerCtx } from '@milkdown/plugin-listener';
  import { nordLight } from '@milkdown/theme-nord';

  import 'material-icons/iconfont/material-icons.css';
  import 'katex/dist/katex.min.css';

  export let defaultValue: string;
  export let onChange: (markdown: string) => void = () => {};
  export let readonly = false;

  let editor: Editor;

  $: {
    if(editor) editor.action(replaceAll(defaultValue));
  }

  async function createEditor(dom: HTMLDivElement) {
    editor = await Editor
      .make()
      .config((ctx) => {
          ctx.set(rootCtx, dom);
          ctx.set(defaultValueCtx, defaultValue);
          ctx.get(listenerCtx).markdownUpdated((ctx, markdown, prevMarkdown) => {
            onChange(markdown);
          });
      })
      .config((ctx) => {
        ctx.update(editorViewOptionsCtx, (prev) => ({
          ...prev,
          editable: () => !readonly,
        }))
      })
      .use(nordLight)
      .use(commonmark)
      .use(gfm)
      .use(listener)
      .use(math)
      .use(clipboard)
      .use(history)
      .use(upload)
      .create();
  }

  function milkdown(dom: HTMLDivElement) {
    createEditor(dom);
  }

</script>

<div use:milkdown />