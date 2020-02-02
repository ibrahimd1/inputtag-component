<template>
  <div class="tag-container">
    <app-tag
      v-for="(tag,index) in tags"
      :key="index"
      :tag="tag"
      :index="index"
      @removeOneTagEvent="removeOneTag($event)"
    ></app-tag>
    <input type="text" @keydown.enter="addTag" @keydown.backspace="removeTag" />
    <div class="error" v-if="error">Bu etiket daha önce eklenmiş!</div>
  </div>
</template>

<script>
import Tag from "./Tag";
export default {
  components: {
    appTag: Tag
  },
  data() {
    return {
      tags: [],
      error: false
    };
  },
  methods: {
    addTag(event) {
      let text = event.target;
      let matchedTag = false;

      if (text.value.length > 0) {
        this.tags.forEach(element => {
          if (element.toLowerCase() === text.value.toLowerCase()) {
            matchedTag = true;
          }
        });
      }

      if (!matchedTag) {
        this.tags.push(text.value);
        text.value = "";
      } else {
        this.error = true;
        setTimeout(() => {
          this.error = false;
        }, 2000);
      }
    },
    removeTag(e) {
      if (e.target.value <= 0) {
        this.tags.splice(this.tags.length - 1, 1);
      }
    },
    removeOneTag(index) {
      this.tags.splice(index, 1);
    }
  },
  props: {
    value: {
      requires: false
    }
  },
  created() {
    if (this.value) {
      if (this.value.length > 0) {
        this.tags = this.value.split(",");
      }
    }
  },
  watch: {
    tags() {
      this.$emit("input", this.tags.join(","));
    }
  }
};
</script>

<style scoped>
input {
  outline: none;
  height: 30px;
  width: 100px;
}

.error {
  font-size: 12px;
  color: darkred;
  margin-top: 5px;
}

.tag-container {
  border: 1px solid #ccc;
  padding: 20px;
}
</style>