<template>
  <div class="container">
    <app-tags v-model="tags" color="success"></app-tags>
    {{ tags }}
  </div>
</template>

<script>
import Tags from "./components/Tags";
export default {
  components: {
    appTags: Tags
  },
  data() {
    return {
      tags: "deneme,test,merhaba"
    };
  }
};
</script>

<style>
body {
  font-family: sans-serif;
}
</style>
