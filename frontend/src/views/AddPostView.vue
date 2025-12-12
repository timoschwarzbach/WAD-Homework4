<script>
export default {
  name: "AddPostData",
  data: () => {
    return {
      postDesc: "",
    };
  },
  methods: {
    addPost: function () {
      fetch("http://localhost:3000/post", {
        headers: {
          "Content-Type": "application/json",
        },
        method: "POST",
        credentials: "include",
        body: JSON.stringify({
          postBody: this.postDesc,
        }),
      }).then(() => location.assign("/"));
    },
  },
};
</script>

<template>
  <div class="post_input">
    <label for="post_input">Post body</label>
    <textarea
      name="fbody"
      id="post_input"
      placeholder="textarea"
      required
      v-model="postDesc"
    ></textarea>
  </div>
  <input type="submit" id="submit_button" @click="addPost" value="Add" />
</template>
