<template>
  <v-app>
    <site-header/>
    <v-main>
    <siteHome/>
    </v-main>
  </v-app>
</template>

<script>
import SiteHeader from './components/siteHeader.vue';
import siteHome from './components/siteHome.vue'

export default {
  name: 'App',

  components: {
    siteHome,
    SiteHeader
  },

  data: () => ({
    //
  }),
};
</script>

<style>

</style>