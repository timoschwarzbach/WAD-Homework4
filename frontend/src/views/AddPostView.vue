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
  <div>
    <div class="post_input">
      <label for="post_input">Add Post</label>
      <div class="input_area">
        <label for="post_input">Body</label>
        <textarea
          name="fbody"
          id="post_input"
          placeholder="textarea"
          required
          v-model="postDesc"
        ></textarea>
      </div>
      <input type="submit" id="submit_button" @click="addPost" value="Add" />
    </div>
  </div>
</template>

<style>
.post_input {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  background-color: #ecf1e2;
  border-radius: 12px;
  max-width: 300px;
  padding: 4px;
  margin: 0 auto;
}

.post_input > label {
  padding: 10px 0;
}

.input_area {
  flex-direction: row;
  vertical-align: middle;
  margin-left: auto;
  margin-right: 10px;
  display: flex;
  align-items: center;
}

.input_area > label {
  padding: 0 40px;
}

textarea {
  background-color: ghostwhite;
  border: none;
  border-radius: 12px;
  text-align: center;
  margin: 5px;
  padding: 10px 0;
  resize: none;
  width: 170px;
  height: 32px;
  overflow: hidden;
}

input {
  background-color: cornflowerblue;
  border-radius: 12px;
  border: none;
  padding: 6px 12px;
  font-size: 16px;
  margin: 10px;
}
</style>