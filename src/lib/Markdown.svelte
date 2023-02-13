<script lang="ts">
  import { Editor, rootCtx, defaultValueCtx } from '@milkdown/core';
  import type { DefaultValue, JSONRecord } from '@milkdown/core';
  import { commonmark } from '@milkdown/preset-commonmark';
  import { gfm } from '@milkdown/preset-gfm';
  import { math } from '@milkdown/plugin-math';
  import { clipboard } from '@milkdown/plugin-clipboard';
  import { upload } from '@milkdown/plugin-upload';
  import { history } from '@milkdown/plugin-history';
  import { listener, listenerCtx } from '@milkdown/plugin-listener';
  import { nord } from '@milkdown/theme-nord';

  import 'material-icons/iconfont/material-icons.css';
  import 'katex/dist/katex.min.css';

  export let defaultValue: DefaultValue;
  export let onChange: (value: {type: 'json', value: JSONRecord}) => void;

  function editor(dom: any) {
      Editor.make()
          .config((ctx) => {
              ctx.set(rootCtx, dom);
              ctx.set(defaultValueCtx, defaultValue);
              ctx.get(listenerCtx).updated((ctx, doc, prevDoc) => {
                onChange(doc.toJSON());
              });
          })
          .use(nord)
          .use(commonmark)
          .use(gfm)
          .use(listener)
          .use(math)
          .use(clipboard)
          .use(history)
          .use(upload)
          .create();
  }
</script>

<style></style>

<div use:editor />