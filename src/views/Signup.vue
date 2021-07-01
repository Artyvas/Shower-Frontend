
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
.my-dropdown-toggle {
  border-radius: 5px;

  ::v-deep .dropdown-toggle {
    color: tomato;
    font-size: 25px;
    font-weight: 800;
  }

  ::v-deep .dropdown-toggle-placeholder {
    color: #c4c4c4;
  }
}
</style>