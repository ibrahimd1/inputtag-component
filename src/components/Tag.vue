<template>
  <span class="tag">
    <span class="content">{{ tag }}</span>
    <span class="close" @click="removeThisTag(index)">X</span>
  </span>
</template>

<script>
export default {
  props: ["tag", "index"],
  methods: {
    removeThisTag(index) {
      this.$emit("removeOneTagEvent", index);
    }
  }
};
</script>

<style scoped>
.tag {
  background-color: #fbdd08;
  padding: 10px;
  color: #000;
  cursor: default;
  margin-right: 10px;
}

.tag * {
  font-size: 14px;
}

.tag .close {
  font-size: 12px;
  cursor: pointer;
}
</style>