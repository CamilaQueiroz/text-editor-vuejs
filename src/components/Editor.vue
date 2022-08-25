<template>
  <div class="row">
    <vue-editor
      id="editor"
      useCustomImageHandler
      @image-added="handleImageAdded"
      v-model="content"
    ></vue-editor>
    <div id="html"></div>
  </div>
</template>

<script>
import { VueEditor } from "vue2-editor";

export default {
  components: {
    VueEditor,
  },

  data() {
    return {
      content: "<h1>Some initial content</h1>",
      imageUrl: "",
    };
  },
  watch: {
    content(newValue) {
      document.getElementById("html").innerHTML = newValue;
    },
  },
  methods: {
    async handleImageAdded(file, Editor, cursorLocation, resetUploader) {
      var reader = new FileReader();
      reader.readAsDataURL(file);
      reader.onload = function () {
        Editor.insertEmbed(cursorLocation, "image", reader.result);
        resetUploader();
      };
      reader.onerror = function (error) {
        return error;
      };
    },
  },
};
</script>
