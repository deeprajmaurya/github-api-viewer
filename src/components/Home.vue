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
          (this.profile.name = json_data.login),
            (this.profile.avatar = json_data.avatar_url),
            (this.profile.repos = json_data.public_repos),
            (this.profile.followers = json_data.followers),
            (this.profile.following = json_data.following),
            (this.profile.homeURL = json_data.url),
            (this.profile.message = json_data.message);
        })
        .catch(error => {
          this.error = error;
        });
    },
    onSearch() {
      this.getProfile(this.username);
    }
  }
};
</script>
