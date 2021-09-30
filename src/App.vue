<template>
  <v-app>
    <v-main>
      <!-- <the-home /> -->
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
// import TheHome from "./views/TheHome.vue";
export default {
  components: {
    // TheHome,
  },
  name: "App",

  data: () => ({
    //
  }),
};
</script>
