<template>
  <vueEditor/>
</template>

<script>
// Advanced Use - Hook into Quill's API for Custom Functionality
import { VueEditor, Quill } from "vue2-editor";
    export default {
        components:{
            VueEditor,
            Quill
        }
    }
</script>

<style lang="css">
    @import "~vue2-editor/dist/vue2-editor.css";
    /* Import the Quill styles you want */
    @import '~quill/dist/quill.core.css';
    @import '~quill/dist/quill.bubble.css';
    @import '~quill/dist/quill.snow.css';
</style>