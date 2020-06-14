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
      console.log(this.profileData);
      return `${GIT}/${this.name}/repositories`;
    },
    profileLink() {
      return `${GIT}/${this.name}`;
    },
    profound() {
      return this.message === "Not Found";
    }
  }
};
</script>

<style scoped>
.notfound {
  background: #fff;
  padding: 1.875rem;
  text-align: center;
}
.notfound h2 {
  font-size: 2rem;
  color: #27ae60;
  margin-bottom: 0.625rem;
}
.notfound p {
  font-size: 1rem;
  color: #000;
}

.github-profile-info {
  background: #fff;
  text-align: center;
  padding: 20px;
}
.github-profile-info img {
  width: 150px;
  height: 150px;
  display: block;
}
.github-profile-info h2 a {
  font-size: 30px;
  color: #2368bd;
}
.github-profile-info h3 {
  font-size: 1.1885rem;
  color: #bdcbce;
}
.github-profile-state {
  background: #34495e;
  text-align: center;
  padding: 1.875rem 0.9375rem;
}
.github-profile-state ul {
  direction: ltr;
}
.github-profile-state li {
  list-style: none;
  display: inline-block;
  margin-right: 1rem;
}

.github-profile-state a {
  color: #fff;
}
.github-profile-state i {
  font-size: 1.5rem;
  font-weight: 700;
  font-style: normal;
  display: block;
}
.github-profile-state span {
  font-size: 20px;
  letter-spacing: 0.06rem;
  color: #27ae60;
}
</style>
