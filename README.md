# ckeditor
## isntall
### library 
npm install @ckeditor/ckeditor5-autoformat@41.1.0 @ckeditor/ckeditor5-basic-styles@41.1.0 @ckeditor/ckeditor5-block-quote@41.1.0 @ckeditor/ckeditor5-build-classic@41.1.0 @ckeditor/ckeditor5-ckbox@41.1.0 @ckeditor/ckeditor5-cloud-services@41.1.0 @ckeditor/ckeditor5-core@41.1.0 @ckeditor/ckeditor5-document-outline@41.1.0 @ckeditor/ckeditor5-editor-classic@41.1.0 @ckeditor/ckeditor5-essentials@41.1.0 @ckeditor/ckeditor5-heading@41.1.0 @ckeditor/ckeditor5-image@41.1.0 @ckeditor/ckeditor5-indent@41.1.0 @ckeditor/ckeditor5-link@41.1.0 @ckeditor/ckeditor5-list@41.1.0 @ckeditor/ckeditor5-media-embed@41.1.0 @ckeditor/ckeditor5-paragraph@41.1.0 @ckeditor/ckeditor5-paste-from-office@41.1.0 @ckeditor/ckeditor5-table@41.1.0 @ckeditor/ckeditor5-theme-lark@41.1.0 @ckeditor/ckeditor5-typing@41.1.0 @ckeditor/ckeditor5-ui@41.1.0 @ckeditor/ckeditor5-undo@41.1.0 @ckeditor/ckeditor5-upload@41.1.0 @ckeditor/ckeditor5-vue@5.1.0 @ckeditor/vite-plugin-ckeditor5@0.1.3
##install this library 
vite-svg-loader
##nuxt config 
### import 
const larkTheme = require.resolve("@ckeditor/ckeditor5-theme-lark");
import svgLoader from "vite-svg-loader";
import ckeditor5 from "@ckeditor/vite-plugin-ckeditor5";

### setup
vite: {
 
      plugins: [
        ckeditor5({
          theme: larkTheme,
        }),
        svgLoader(),
      ],
  },
### create plugin file = ckeditor.client.ts
## write code

import CKEditor from "@ckeditor/ckeditor5-vue";
// import ClassicEditor from "@ckeditor/ckeditor5-build-classic";
import Editor from "~/lib/CustomEditor";

export default defineNuxtPlugin((nuxtApp) => {
    nuxtApp.vueApp.use(CKEditor);
    return {
        provide: {
            ckeditor: {
                customEditor: Editor,
                // classicEditor: ClassicEditor,
            },
        },
    };
});

##create folder lib and create CustomEditor.ts 
/**
 * @license Copyright (c) 2014-2024, CKSource Holding sp. z o.o. All rights reserved.
 * For licensing, see LICENSE.md or https://ckeditor.com/legal/ckeditor-oss-license
 */

import { ClassicEditor } from '@ckeditor/ckeditor5-editor-classic';

import { Autoformat } from '@ckeditor/ckeditor5-autoformat';
import { Bold, Italic } from '@ckeditor/ckeditor5-basic-styles';
import { BlockQuote } from '@ckeditor/ckeditor5-block-quote';
import { CKBox } from '@ckeditor/ckeditor5-ckbox';
import { CloudServices } from '@ckeditor/ckeditor5-cloud-services';
import type { EditorConfig } from '@ckeditor/ckeditor5-core';
import { Essentials } from '@ckeditor/ckeditor5-essentials';
import { Heading } from '@ckeditor/ckeditor5-heading';
import {
    Image,
    ImageCaption,
    ImageStyle,
    ImageToolbar,
    ImageUpload,
    PictureEditing
} from '@ckeditor/ckeditor5-image';
import { Indent } from '@ckeditor/ckeditor5-indent';
import { Link } from '@ckeditor/ckeditor5-link';
import { List } from '@ckeditor/ckeditor5-list';
import { MediaEmbed } from '@ckeditor/ckeditor5-media-embed';
import { Paragraph } from '@ckeditor/ckeditor5-paragraph';
import { PasteFromOffice } from '@ckeditor/ckeditor5-paste-from-office';
import {
    Table,
    TableCaption,
    TableCellProperties,
    TableColumnResize,
    TableProperties,
    TableToolbar
} from '@ckeditor/ckeditor5-table';
import { TextTransformation } from '@ckeditor/ckeditor5-typing';
import { Undo } from '@ckeditor/ckeditor5-undo';
import { Base64UploadAdapter } from '@ckeditor/ckeditor5-upload';

// You can read more about extending the build with additional plugins in the "Installing plugins" guide.
// See https://ckeditor.com/docs/ckeditor5/latest/installation/plugins/installing-plugins.html for details.

class Editor extends ClassicEditor {
    public static override builtinPlugins = [
        Autoformat,
        BlockQuote,
        Base64UploadAdapter,
        Bold,
        CKBox,
        CloudServices,
        Essentials,
        Heading,
        Image,
        ImageCaption,
        ImageStyle,
        ImageToolbar,
        ImageUpload,
        Indent,
        Italic,
        Link,
        List,
        MediaEmbed,
        Paragraph,
        PasteFromOffice,
        PictureEditing,
        Table,
        TableCaption,
        TableCellProperties,
        TableColumnResize,
        TableProperties,
        TableToolbar,
        TextTransformation,
        Undo
    ];

    public static override defaultConfig: EditorConfig = {
        toolbar: {
            items: [
                'heading',
                '|',
                'bold',
                'italic',
                'link',
                'bulletedList',
                'numberedList',
                '|',
                'outdent',
                'indent',
                '|',
                'imageUpload',
                'insertTable',
                'blockQuote',
                'undo',
                'redo'
            ]
        },
        language: 'en',
        image: {
            toolbar: [
                'imageTextAlternative',
                'toggleImageCaption',
                'imageStyle:inline',
                'imageStyle:block',
                'imageStyle:side'
            ]
        },
        table: {
            contentToolbar: [
                'tableColumn',
                'tableRow',
                'mergeTableCells',
                'tableCellProperties',
                'tableProperties'
            ]
        }
    };
}

export default Editor;

## create component editor 
<template>
  <ckeditor :editor="editor" :value="value" @input="emitInput" />
</template>

<script setup>
defineProps({
  value: {
    type: String
  }
})
const emit = defineEmits(['input'])
const emitInput = (event) => {
  emit("input", event)
}
const { $ckeditor } = useNuxtApp()
const editor = $ckeditor.customEditor;

</script>

## import to file wanna working 
<template>
  <div>
    <h1 class="container mt-3 mb-3">Sample CKEditor with Nuxt.js</h1>
    <div class="container">
      <rich-editor :value="editorInput" @input="event => editorInput = event" />
    </div>
    <div class="container mt-3">
      <div class="row">
        <h2 class="col-md-12">Output</h2>
        <div>{{ editorInput }}</div>
      </div>
    </div>
    <div class="container mt-3">
      <div class="row">
        <h2 class="col-md-12">Preview</h2>
        <div v-html="editorInput"></div>
      </div>
    </div>
  </div>
</template>
<style>
/* page-with-editor.css */
body .ck-content .table table, body .ck-content .table td {
  border: dotted 1px #ddd;
}

/* page-with-editor-content.css */
body .ck-content .table table, body .ck-content .table td {
  border: none;
}
</style>
<script>

export default {
  data() {
    return {
      editorInput: ''
    }
  },
}
</script>


##End
-------------> Thank you
  
