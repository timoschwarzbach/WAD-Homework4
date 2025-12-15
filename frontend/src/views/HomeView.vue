<template>
  <div>
    <div class="container">
      <button v-if="authResult" @click="Logout" class="center">Logout</button>
    </div>
    <div class="posts">
      <div
        class="post"
        @click="updatePost(post.id)"
        v-for="post in posts"
        :key="post.id"
      >
        <span>{{
          new Date(post.created_at).toLocaleString("en-US", {
            month: "short",
            day: "numeric",
            year: "numeric",
          })
        }}</span>
        <p>{{ post.body }}</p>
      </div>
    </div>
    <div class="actions">
      <button @click="this.$router.push('/add')">Add post</button>
      <button @click="deleteAll" v-if="posts.length > 0">Delete all</button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import auth from "../auth";

export default {
  name: "HomeView",
  components: {},
  data: function () {
    return {
      posts: [],
      authResult: auth.authenticated(),
    };
  },
  methods: {
    Logout() {
      fetch("http://localhost:3000/auth/logout", {
        credentials: "include", //  Don't forget to specify this if you need cookies
      })
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          console.log("jwt removed");
          //console.log('jwt removed:' + auth.authenticated());
          this.$router.push("/login");
          //location.assign("/");
        })
        .catch((e) => {
          console.log(e);
          console.log("error logout");
        });
    },
    deleteAll() {
      fetch("http://localhost:3000/post", {
        method: "DELETE",
        credentials: "include",
      }).then(() => {
        this.posts = [];
      });
    },
    updatePost(id) {
      this.$router.push("/post/" + id);
    },
  },
  mounted() {
    fetch("http://localhost:3000/post", {
      credentials: "include",
    })
      .then((response) => response.json())
      .then(
        (data) =>
          (this.posts = data.sort((a, b) =>
            b.created_at.localeCompare(a.created_at)
          ))
      )
      .catch((err) => console.log(err.message));
  },
};
</script>

<style scoped>
.posts {
  max-width: 400px;
  margin: 0 auto;
}

body {
  margin: 20px 40px;
  font-size: 1.2rem;
  letter-spacing: 1px;
  background: #fafafa;
  position: relative;
}

h3 {
  margin: 0;
  padding: 0;
  font-family: "Quicksand", sans-serif;
  color: #444;
  background: #7e9756;
}

h1,
h2,
h3,
h4,
ul,
li,
a,
input,
label,
button,
div,
footer {
  margin: 0;
  padding: 0;
  font-family: "Quicksand", sans-serif;
  color: #444;
}
nav {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 80px;
}
input {
  padding: 10px 12px;
  border-radius: 4px;
  border: 1px solid #ddd;
  font-size: 1em;
  width: 100%;
}
label {
  display: block;
  margin: 20px 0 10px;
}
button {
  background-color: cornflowerblue;
  border-radius: 12px;
  border: none;
  padding: 6px 12px;
  font-size: 16px;
  margin: 10px;
}
nav {
  display: flex;
  align-items: center;
}

.actions {
  flex-direction: row;
  display: flex;
  justify-content: center;
}

.post {
  border-radius: 12px;
  background-color: #d8d8d8;
  padding: 4px;
  margin: 12px 0;
  max-width: 400px;
}

.post > div {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.container {
  display: flex;
  justify-content: center;
}
</style>
