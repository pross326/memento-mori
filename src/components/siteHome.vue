<template>
  <v-container class="grey darken-4 fill-height" fluid>
    <v-row class="ma-8">
      <v-col cols="3">
        <v-card class="d-flex align-center rounded-lg flex-column pa-1">
          <v-card-title class="text-h4"> Choose your birthday. </v-card-title>
          <v-date-picker v-model="picker"></v-date-picker>
        </v-card>
        <v-card class="d-flex align-center rounded-lg flex-column pa-1 mt-5">
          <v-card-title class="text-h4"> Choose your lifespan. </v-card-title>
          <v-card-text>
            <v-slider
              v-model="value"
              step="10"
              min="60"
              thumb-label
              ticks
            ></v-slider>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="6">
        <v-card class="fill-height rounded-lg"> testing </v-card>
      </v-col>
      <v-col cols="3">
        <v-card class="rounded-lg ">
          <v-card-title class="text-h4">Age: {{picker}}</v-card-title>
          </v-card>
        <v-card class="rounded-lg mt-5 mb-5">
          <v-card-title class="text-h4">Predicted Lifespan: {{value}}</v-card-title>
          </v-card>
        <v-card class="rounded-lg">
          <v-card-title class="text-h4">Weeks Remaining: {{weeks}}</v-card-title>
          </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "siteHome",
  data: () => ({
    picker: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    value: 80,
  }),
  weeks: [6],
  picker: '',
};

</script>

<style></style>
