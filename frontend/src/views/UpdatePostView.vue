<template>
  <div>
    <div class="post_input">
      <label for="post_input">A Post</label>
      <div class="input_area">
        <label for="post_input">Body</label>
        <textarea
          name="fbody"
          id="post_input"
          placeholder="textarea"
          required
          v-model="postBody"
        ></textarea>
      </div>
      <div class="row">
        <input
          type="submit"
          id="submit_button"
          @click="updatePost"
          value="Update"
        />
        <input
          type="submit"
          id="submit_button"
          @click="deletePost"
          value="Delete"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UpdatePostData",
  data: function () {
    return {
      postBody: "Loading...",
      postCreated: new Date(),
    };
  },
  props: {
    id: String,
  },
  methods: {
    updatePost: function () {
      fetch(`http://localhost:3000/post/${this.id}`, {
        headers: {
          "Content-Type": "application/json",
        },
        method: "PUT",
        credentials: "include",
        body: JSON.stringify({
          postBody: this.postBody,
        }),
      }).then(() => location.assign("/"));
    },
    deletePost: function () {
      fetch(`http://localhost:3000/post/${this.id}`, {
        headers: {
          "Content-Type": "application/json",
        },
        method: "DELETE",
        credentials: "include",
        body: JSON.stringify({
          postBody: this.postBody,
        }),
      }).then(() => location.assign("/"));
    },
  },
  mounted() {
    fetch(`http://localhost:3000/post/${this.id}`, {
      credentials: "include",
    })
      .then((response) => response.json())
      .then((data) => {
        this.postBody = data.body;
        // this.postCreated = data.created_at;
      })
      .catch((err) => console.log(err.message));
  },
};
</script>

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
