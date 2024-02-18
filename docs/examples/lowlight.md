---
title: Code Block Lowlight Example
---

# Code Block Lowlight Example

This example uses Code Block with `lowlight` for syntax highlighting.

::: tip INSTALLED BY PLUGIN
The extension is already installed by default with Nuxt Tiptap Editor plugin.
:::

`lowlight` is a option that can be enabled in the configuration. Until `lowlight` option evaluates to `true`, `lowlight` related objects won't be imported to the project to reduce chunk size.

**More about [Code Block Lowlight Extension](https://tiptap.dev/docs/editor/api/nodes/code-block-lowlight).**

1. Configuration

   ```js
   export default defineNuxtConfig({
     modules: ["nuxt-tiptap-editor"],
     tiptap: {
       prefix: "Tiptap", //prefix for Tiptap components
       lowlight: {
         theme: "github-dark",
       },
     },
   });
   ```

   Check this [file](https://github.com/modbender/nuxt-tiptap-editor/blob/7dfbe1c213af472f8f7a50b0e3dd5a7dd8552ce9/src/types.d.ts#L3) for full list of themes.

2. There are 2 types of lowlight syntax highlight language preset - `common` and `full`.  
   Adding to the prefix in configuration it becomes `Tiptapcommon` and `Tiptapfull`.

   ```js
   const lowlight = TiptapcreateLowlight(Tiptapcommon); //Common languages

   // or

   const lowlight = TiptapcreateLowlight(Tiptapall); //All languages
   ```

   Copy the code to your own `components/TiptapEditor.vue`.  
   Any path is fine as long as it's under `components` directory with `.vue` extension.

   ```vue
   <template>
     <div>
       <div v-if="editor">
         <button
           @click="editor.chain().focus().toggleBold().run()"
           :disabled="!editor.can().chain().focus().toggleBold().run()"
           :class="{ 'is-active': editor.isActive('bold') }"
         >
           bold
         </button>
         <button
           @click="editor.chain().focus().toggleItalic().run()"
           :disabled="!editor.can().chain().focus().toggleItalic().run()"
           :class="{ 'is-active': editor.isActive('italic') }"
         >
           italic
         </button>
         <button
           @click="editor.chain().focus().toggleStrike().run()"
           :disabled="!editor.can().chain().focus().toggleStrike().run()"
           :class="{ 'is-active': editor.isActive('strike') }"
         >
           strike
         </button>
         <button
           @click="editor.chain().focus().toggleCode().run()"
           :disabled="!editor.can().chain().focus().toggleCode().run()"
           :class="{ 'is-active': editor.isActive('code') }"
         >
           code
         </button>
         <button @click="editor.chain().focus().unsetAllMarks().run()">
           clear marks
         </button>
         <button @click="editor.chain().focus().clearNodes().run()">
           clear nodes
         </button>
         <button
           @click="editor.chain().focus().setParagraph().run()"
           :class="{ 'is-active': editor.isActive('paragraph') }"
         >
           paragraph
         </button>
         <button
           @click="editor.chain().focus().toggleHeading({ level: 1 }).run()"
           :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }"
         >
           h1
         </button>
         <button
           @click="editor.chain().focus().toggleHeading({ level: 2 }).run()"
           :class="{ 'is-active': editor.isActive('heading', { level: 2 }) }"
         >
           h2
         </button>
         <button
           @click="editor.chain().focus().toggleHeading({ level: 3 }).run()"
           :class="{ 'is-active': editor.isActive('heading', { level: 3 }) }"
         >
           h3
         </button>
         <button
           @click="editor.chain().focus().toggleHeading({ level: 4 }).run()"
           :class="{ 'is-active': editor.isActive('heading', { level: 4 }) }"
         >
           h4
         </button>
         <button
           @click="editor.chain().focus().toggleHeading({ level: 5 }).run()"
           :class="{ 'is-active': editor.isActive('heading', { level: 5 }) }"
         >
           h5
         </button>
         <button
           @click="editor.chain().focus().toggleHeading({ level: 6 }).run()"
           :class="{ 'is-active': editor.isActive('heading', { level: 6 }) }"
         >
           h6
         </button>
         <button
           @click="editor.chain().focus().toggleBulletList().run()"
           :class="{ 'is-active': editor.isActive('bulletList') }"
         >
           bullet list
         </button>
         <button
           @click="editor.chain().focus().toggleOrderedList().run()"
           :class="{ 'is-active': editor.isActive('orderedList') }"
         >
           ordered list
         </button>
         <button
           @click="editor.chain().focus().toggleCodeBlock().run()"
           :class="{ 'is-active': editor.isActive('codeBlock') }"
         >
           code block
         </button>
         <button
           @click="editor.chain().focus().toggleBlockquote().run()"
           :class="{ 'is-active': editor.isActive('blockquote') }"
         >
           blockquote
         </button>
         <button @click="editor.chain().focus().setHorizontalRule().run()">
           horizontal rule
         </button>
         <button @click="editor.chain().focus().setHardBreak().run()">
           hard break
         </button>
         <button
           @click="editor.chain().focus().undo().run()"
           :disabled="!editor.can().chain().focus().undo().run()"
         >
           undo
         </button>
         <button
           @click="editor.chain().focus().redo().run()"
           :disabled="!editor.can().chain().focus().redo().run()"
         >
           redo
         </button>
       </div>
       <TiptapEditorContent :editor="editor" />
     </div>
   </template>

   <script setup>
   const lowlight = TiptapcreateLowlight(Tiptapall);

   const editor = useEditor({
     extensions: [
       TiptapStarterKit.configure({
         codeBlock: false,
       }),
       TiptapCodeBlockLowlight.configure({ lowlight }),
     ],
   });
   </script>
   ```