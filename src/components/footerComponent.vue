<template>
  <v-footer color="grey darken-2" padless test>
    <v-row class="ma-0 white--text">
      <v-col class="text-center">
        <p>Copyright &copy; {{ currentYear }} Paul Ross</p>
      </v-col>
      <v-col class="text-center">
        <p id="email-link" >
          <a class="white--text" href="mailto:pross326@gmail.com">Contact Me</a>
        </p>
      </v-col>
    </v-row>
  </v-footer>
</template>

<script>
export default {
  name: "FooterComponent",
  data: () => ({
    currentYear: new Date().getFullYear(),
  }),
};
</script>

<style>
p {
  margin-bottom: 0px !important;
}

#email-link a{
  text-decoration: none;
}
</style>
