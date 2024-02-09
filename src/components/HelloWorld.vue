<script>
import grapesjs from 'grapesjs'
import 'grapesjs/dist/css/grapes.min.css'
import 'grapesjs/dist/grapes.min.js'
// import 'grapesjs-preset-webpage/dist/grapesjs-preset-webpage.min.css'
import webpagePlugin from  'grapesjs-preset-webpage'
import basicBlocksPlugin from 'grapesjs-blocks-basic'
import exportBlocksPlugin from 'grapesjs-plugin-export'
import imageEditorPlugin from 'grapesjs-tui-image-editor';
import ckeditor from 'grapesjs-plugin-ckeditor';

export default {
 name: 'WebBuilder',

 mounted(){
   const editor = grapesjs.init({
     container: '#gjs',
     height: '900px',
     width: '100%',
     plugins: [basicBlocksPlugin, webpagePlugin, exportBlocksPlugin, imageEditorPlugin, ckeditor],
     storageManager: {
       id: 'gjs-',
       type: 'local',
       autosave: false,
       storeComponents: true,
       storeStyles: true,
       storeHtml: true,
       storeCss: true,
     },
     deviceManager: {
       devices:
       [
         {
           id: 'desktop',
           name: 'Desktop',
           width: '',
         },
         {
           id: 'tablet',
           name: 'Tablet',
           width: '768px',
           widthMedia: '992px',
         },
         {
           id: 'mobilePortrait',
           name: 'Mobile portrait',
           width: '320px',
           widthMedia: '575px',
         },
       ]
     },
     pluginsOpts: {
       'grapesjs-preset-webpage': {
         blocksBasicOpts: {
           blocks: ['column1', 'column2', 'column3', 'column3-7', 'text',     'link', 'image', 'video'],
           flexGrid: 1,
         },
         blocks: ['link-block', 'quote', 'text-basic'],
         exportBlocksPlugin: {addExportBtn: true, btnLabel: "Export to ZIP"},

         imageEditorPlugin: {},
         ckeditor: {}
       },
     }
   })
   editor.runCommand(exportBlocksPlugin);
 }
}
</script>

<template>
<div id="gjs"></div>
</template>

<style scoped>
.header {
  background-color: #333;
  color: #fff;
  padding: 20px;
}

.container {
  display: flex;
}
 
.sidebar {
  width: 30%;
  background-color: #f2f2f2;
  padding: 20px;
}

.main-content {
  width: 70%;
  padding: 20px;
}
</style>
