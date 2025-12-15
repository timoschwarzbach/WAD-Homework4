<template>
  <div>
    <form @submit.prevent="SignUp" class="form">
      <div class="input_area">
        <label for="email">Email</label>
        <input
          type="email"
          name="email"
          placeholder="Email"
          required
          v-model="email"
        />
      </div>
      <div class="input_area">
        <label for="password">Password</label>
        <input
          type="password"
          name="password"
          placeholder="Password"
          required
          v-model="password"
        />
      </div>
      <button type="submit" class="SignUp">SignUp</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "SignUp",

  data: function () {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    SignUp() {
      var data = {
        email: this.email,
        password: this.password,
      };
      // using Fetch - post method - send an HTTP post request to the specified URI with the defined body
      fetch("http://localhost:3000/auth/signup", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        credentials: "include", //  Don't forget to specify this if you need cookies
        body: JSON.stringify(data),
      })
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          this.$router.push("/");
          //location.assign("/");
        })
        .catch((e) => {
          console.log(e);
          console.log("error");
        });
    },
  },
};
</script>

<style scoped>
.form {
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

.form > label {
  padding: 10px 0;
}

input {
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

button {
  background-color: cornflowerblue;
  border-radius: 12px;
  border: none;
  padding: 6px 12px;
  font-size: 16px;
  margin: 10px;
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
  margin-right: 20px;
}
</style>
