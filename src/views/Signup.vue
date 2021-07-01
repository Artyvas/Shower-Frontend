
<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>First name:</label>
        <input type="text" class="form-control" v-model="first_name" />
        <small>{{ 20 - first_name.length }} characters remaining</small>
      </div>
      <div class="form-group">
        <label>Last name:</label>
        <input type="text" class="form-control" v-model="last_name" />
        <small>{{ 40 - last_name.length }} characters remaining</small>
      </div>
      <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="email" />
      </div>
      <div class="form-group">
        <label>Password:</label>
        <input type="password" class="form-control" v-model="password" />
        <small v-if="password.length > 0 && password.length < 6" class="text-danger">
          Password must be at least 6 characters
        </small>
      </div>
      <div class="form-group">
        <label>Password confirmation:</label>
        <input type="password" class="form-control" v-model="passwordConfirmation" />
        <small v-if="passwordConfirmation !== password" class="text-danger">Passwords must match!</small>
      </div>
      <div class="form-group">
        <label>Date of Birth:</label>
        <input type="date" class="form-control" v-model="dob" />
      </div>
      <div class="form-group">
        <label>Gender:</label>
        <input type="text" class="form-control" v-model="gender" />
      </div>

      <div class="form-group">
        <label>Mountain Project Username:</label>
        <input type="text" class="form-control" v-model="mp_username" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      first_name: "",
      last_name: "",
      mp_username: "",
      flagged: false,
      dob: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        first_name: this.first_name,
        last_name: this.last_name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
        dob: this.dob,
        gender: this.gender,
        mp_username: this.mp_username,
      };
      axios
        .post("/api/users", params)
        .then(response => {
          console.log(response);
          this.$router.push("/login");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<style scoped>
  body {
    background-color: #fafafa !important;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  .signup > div{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    flex-grow: 1;
  }

  .signup{
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0 2%;
    width: 100%;
  }

  .field-wrap, .wrapper{
    width: 100%;
  }

  .dropList{
    z-index: 10;
    background-color: #FFF;
    position: relative;
    width: 40%;
    top: 5px;
    right: 12px;
  }

  .signup{
    margin: 10px 0 20px 18px;
    font-size: 16px;
    font-weight: bold;
    text-align: left;
  }

  .hint{
    font-size: 10px;
    font-style: italic;
    color: purple;
  }

  .help-block{
    color: red;
  }
</style>
