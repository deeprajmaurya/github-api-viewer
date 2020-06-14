<template>
  <div>
    <Profile />
    {{ username }}
  </div>
</template>

<script>
import Profile from "./Profile";
const API = "https://api.github.com/users";

export default {
  name: "Github",
  props: ["username"],
  data() {
    return {
      name: "",
      avatar: "",
      repos: "",
      followers: "",
      following: "",
      homeURL: ""
    };
  },
  components: {
    Profile
  },
  mounted() {
    // API call
    //console.log(this.props);
    if (this.username !== "") {
      this.getProfile(this.username);
    }
  },
  methods: {
    getProfile(username) {
      console.log("get profile called");
      let url = `${API}/${username}`;
      console.log(url);
      fetch(url)
        .then(res => res.json())
        .then(json_data => {
          (this.name = json_data.login),
            (this.avatar = json_data.avatar_url),
            (this.repos = json_data.public_repos),
            (this.followers = json_data.followers),
            (this.following = json_data.following),
            (this.homeURL = json_data.url);
          console.log(json_data);
        })
        .catch(error => {
          this.error = error;
        });
    },
    updateUsername(username) {
      this.username = username;
    }
  }
};
</script>
