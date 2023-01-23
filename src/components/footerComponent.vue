<template>
    <v-footer>
      <v-row class="ma-0">
        <v-col class="text-center">
          <p>Copyright &copy; {{currentYear}} Paul Ross</p>
        </v-col>
        <v-col class="text-center">
          <p>Contact: <a href="mailto:pross326@gmail.com">pross326@gmail.com</a></p>
        </v-col>
      </v-row>
    </v-footer>
  </template>
  
  <script>
  export default {
    name: "FooterComponent",
    data: () => ({
      currentYear: new Date().getFullYear()
    })
  };
  </script>
  