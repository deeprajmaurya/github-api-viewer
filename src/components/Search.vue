<template>
  <v-container>
    <v-card class="mx-8" max-width="900">
      <v-form>
        <v-text-field
          v-model="username"
          v-bind:username="username"
          label="Enter Github username"
          required
        ></v-text-field>
        <v-btn color="warning" type="submit" class="ma-4">
          Search
        </v-btn>
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      username: "deeprajmaurya"
    };
  },
  methods: {
    onSubmit() {
      //
    }
  }
};
</script>
