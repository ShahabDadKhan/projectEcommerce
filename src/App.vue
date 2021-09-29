<template>
  <v-app>
    <v-main>
      <the-home />
    </v-main>
  </v-app>
</template>

<script>
import TheHome from "./views/TheHome.vue";
export default {
  components: {
    TheHome,
  },
  name: "App",

  data: () => ({
    //
  }),
};
</script>
