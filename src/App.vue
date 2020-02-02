<template>
  <div class="tag-container">
    <span class="tag" v-for="(tag,index) in tags" :key="tag">
      <span class="content">{{ tag }}</span>
      <span class="close" @click="removeOneTag(index)">X</span>
    </span>
    <input type="text" @keydown.enter="addTag" @keydown.backspace="removeTag" />
    <div class="error" v-if="error">Bu etiket daha önce eklenmiş!</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tags: ["deneme", "test"],
      error: false
    };
  },
  methods: {
    addTag(event) {
      let text = event.target;
      let matchedTag = false;

      if (text.length > 0) {
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
  }
};
</script>

<style>
body {
  font-family: sans-serif;
}

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

.tag {
  background-color: #fbdd08;
  padding: 10px;
  color: #000;
  cursor: default;
  font-size: 14px;
  margin-right: 10px;
}

.tag .close {
  font-size: 12px;
  cursor: pointer;
}
</style>
