<template>
  <div id="app">
    <PhotoEditor :layout="layout" :license="license" :image-path="path" />
  </div>
</template>

<script>
import PhotoEditor from './components/PhotoEditor.vue';
import { UIEvent } from 'photoeditorsdk';

const myLicense = ''; // replace this with the content of your license file

export default {
  name: 'App',
  components: {
    PhotoEditor
  },
  data: () => ({
    layout: 'advanced',
    license: myLicense,
    path: 'example.jpg'
  }),
  mounted() {
    this.$pesdk.on(UIEvent.EXPORT, result => {
      // eslint-disable-next-line
      console.log(result);
    });
    this.$pesdk.on(UIEvent.EDITOR_READY, () => {
      // You can also access the editor and call functions on it
      // directly if you need to.
      this.$pesdk.getEditor();
    });
  }
};
</script>

<style>
body {
  margin: 0;
}
</style>
