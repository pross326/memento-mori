<template>
  <v-container class="grey darken-4" fluid>
    <v-row class="ma-1">
      <v-spacer></v-spacer>
      <v-col cols="10">
        <v-stepper v-model="e1" height="750">
          <v-stepper-header>
            <v-spacer></v-spacer>
            <v-stepper-step :complete="e1 > 1" step="1">
              Enter Your Birthday
            </v-stepper-step>
            <v-divider></v-divider>
            <v-stepper-step :complete="e1 > 2" step="2">
              Enter Your Life Expectancy
            </v-stepper-step>
            <v-spacer></v-spacer>
          </v-stepper-header>
          <v-stepper-items>
            <v-stepper-content step="1">
              <v-card class="ma-10" color="grey lighten-0">
                <v-card-title class="text-h4">
                  Enter your birthday.
                </v-card-title>
                <v-row>
                  <v-col class="d-flex justify-center">
                    <v-date-picker
                      class="d-flex justify-center rounded-lg mb-10 col-md-6 col-xl-8"
                      @input="picker"
                      v-model="picker"
                    ></v-date-picker>
                  </v-col>
                </v-row>
              </v-card>
              <div class="d-flex justify-center">
                <v-btn color="primary" @click="e1 = 2; emitEvent()"> Continue </v-btn>
              </div>
            </v-stepper-content>
            <v-stepper-content step="2">
              <v-card class="ma-12" color="grey lighten-0">
                <v-card-title class="text-h4">
                  Enter your Life Expectancy.
                </v-card-title>
                <v-card-subtitle> (80 Default) </v-card-subtitle>
                <v-row>
                  <v-spacer></v-spacer>
                  <v-col cols="8" class="justify-center mb-10">
                    <v-card elevation="5">
                      <v-card-title class="text-h2 d-flex justify-center">
                        {{ this.value }} Years
                      </v-card-title>
                      <v-card-text>
                        <v-slider
                          v-model="value"
                          height="150"
                          step="10"
                          min="60"
                          thumb-label
                          ticks
                          class="d-flex justify-center rounded-lg col-md-6 col-xl-8"
                        ></v-slider>
                        <v-card-subtitle class="d-flex justify-center"
                          >Use the slider above</v-card-subtitle
                        >
                      </v-card-text>
                    </v-card>
                  </v-col>
                  <v-spacer></v-spacer>
                </v-row>
              </v-card>
              <div class="d-flex justify-center">
                <v-btn color="primary" class="ma-5" @click="switchComponent()">
                  Continue
                </v-btn>
                <v-btn text class="ma-5" @click="e1 = 1"> Go Back </v-btn>
              </div>
            </v-stepper-content>
          </v-stepper-items>
        </v-stepper>
      </v-col>
      <v-spacer></v-spacer>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "enterData",
  data: () => ({
    picker: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    value: 80,
    e1: 1,
  }),
  props: ["switch-component"],
  methods: {
    emitEvent () {
      this.$emit('pass-data', this.picker)
    },
  },
};
</script>

<style>
.rt-cards {
  word-break: normal;
  max-width: 100%;
}

.e2-card {
  width: 100%;
}
</style>
