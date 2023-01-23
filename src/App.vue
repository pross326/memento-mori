<template>
  <v-app>
    <site-header/>
    <v-main>
    <switcher-component/>
    </v-main>
  </v-app>
</template>

<script>
import SiteHeader from './components/siteHeader.vue';
import SwitcherComponent from './components/switcherComponent.vue';

export default {
  name: 'App',

  components: {
    SiteHeader,
    SwitcherComponent
  },

  data: () => ({
    //
  }),
};
</script>

<style>
*{
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif
}
</style>