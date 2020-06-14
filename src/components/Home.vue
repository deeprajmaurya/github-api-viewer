<template>
  <v-container>
    <v-card max-width="900">
      <form @submit.prevent="onSearch">
        <v-text-field
          v-model="username"
          label="Enter Github username"
          required
          type="search"
        ></v-text-field>
        <v-btn color="warning" type="submit" class="ma-4">
          Search
        </v-btn>
      </form>
    </v-card>
    <Profile v-bind:profile-data="profile" />
  </v-container>
</template>

<script>
const API = "https://api.github.com/users";
import Profile from "./Profile";
export default {
  data() {
    return {
      username: "",
      profile: {
        name: "",
        avatar: "",
        repos: "",
        followers: "",
        following: "",
        homeURL: "",
        message: ""
      }
    };
  },
  components: {
    Profile
  },
  mounted() {
    // API call
    this.getProfile("deeprajmaurya");
  },
  methods: {
    getProfile(username) {
      let url = `${API}/${username}`;
      fetch(url)
        .then(res => res.json())
        .then(json_data => {
          (this.name = json_data.login),
            (this.avatar = json_data.avatar_url),
            (this.repos = json_data.public_repos),
            (this.followers = json_data.followers),
            (this.following = json_data.following),
            (this.homeURL = json_data.url),
            (this.message = json_data.message),
            console.log(json_data);
        })
        .catch(error => {
          console.log(error);
          this.error = error;
        });
    },
    onSearch() {
      this.getProfile(this.username);
    }
  }
};
</script>
