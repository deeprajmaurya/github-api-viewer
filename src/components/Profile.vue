<template>
  <div>
    <v-alert v-if="profound" type="error" class="mt-8" max-width="900">
      Profile not found
    </v-alert>
    <v-container>
      <v-card v-if="!profound" fluid max-width="900">
        <v-row>
          <v-col cols="6">
            <v-avatar size="300px" class="ml-5">
              <img alt="Avatar" :src="profileData.avatar" />
              <v-icon></v-icon>
            </v-avatar>
          </v-col>
          <v-col cols="6">
            <h2>No of Followers : {{ profileData.followers }}</h2>
            <h2>No of Followers : {{ profileData.following }}</h2>
            <v-btn class="ma-2 primary" :href="profileLink" target="_blank">
              Visit Profile
            </v-btn>
            <v-btn tile class="ma-2 primary" :href="reposLink" target="_blank">
              Visit Repos
            </v-btn>
          </v-col>
        </v-row>
      </v-card>
    </v-container>
  </div>
</template>

<script>
const GIT = "https://github.com";
export default {
  name: "Profile",
  props: ["profileData"],
  computed: {
    reposLink() {
      return `${GIT}/${this.profileData.name}/repositories`;
    },
    profileLink() {
      return `${GIT}/${this.profileData.name}`;
    },
    profound() {
      return this.profileData.message === "Not Found";
    }
  }
};
</script>
