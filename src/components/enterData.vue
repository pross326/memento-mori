<template>
  <div>
    <v-row class="justify-center grey darken-4">
      <v-card
        class="col-xs-10 col-sm-10 col-xl-8 justify-center align-center d-flex flex-column text-center" color="#212121" elevation="0"
      >
        <v-card-text id="enterDataIntro" class="text-overline white--text">
          Enter your birth date and life expectancy below for a visual reminder
          to live each day to the fullest.
        </v-card-text>
      </v-card>
    </v-row>
    <v-container class="grey darken-4" fluid height="fill">
      <v-row class="ma-1">
        <v-spacer></v-spacer>
        <v-stepper
          v-model="e1"
          class="backgroundColor col-md-8 col-xs-12"
          elevation="0"
          :style="{ backgroundColor: 'black' }"
        >
          <v-stepper-header class="backgroundColor">
            <v-spacer></v-spacer>
            <v-stepper-step color="#212121" class="overline" :complete="e1 > 1" step="1">
              Date of Birth
            </v-stepper-step>
            <v-divider></v-divider>
            <v-stepper-step color="#212121" class="overline" :complete="e1 > 2" step="2">
              Life Expectancy
            </v-stepper-step>
            <v-spacer></v-spacer>
          </v-stepper-header>
          <v-stepper-items>
            <v-stepper-content step="1" class="align-items backgroundColor">
              <v-card
                height="fill"
                color="grey darken-2"
                elevation="5"
                class="d-flex flex-column align-center mb-5 enterDataCard"
                v-bind:style="{ 'background-image': `url(${backgroundImage})` }"
              >
                <v-card
                  elevation="5"
                  class="col-xl-5 justify-center align-center d-flex flex-column pa-0 mt-3"
                >
                  <v-card-title> Enter your birth date. </v-card-title>
                  <v-card-subtitle>
                    Your birth date is used to calculate how many weeks you've
                    lived.
                  </v-card-subtitle>
                </v-card>
                <v-date-picker
                  elevation="5"
                  class="d-flex justify-center rounded-lg mb-3 mt-3 col-xl-5"
                  @input="picker"
                  v-model="formData.birthDate"
                  header-color="#212121"
                  color="#212121"
                ></v-date-picker>
              </v-card>
              <div class="d-flex justify-center">
                <v-btn :disabled="dateIsValid" color="#C68F55" @click="e1 = 2">
                  Continue
                </v-btn>
              </div>
            </v-stepper-content>
            <v-stepper-content step="2" class="align-items backgroundColor">
              <v-card
                height="fill"
                color="grey darken-2"
                class="d-flex flex-column align-center mb-5 enterDataCard"
                v-bind:style="{ 'background-image': `url(${backgroundImage})` }"
              >
                <v-card
                  elevation="4"
                  class="col-xs-10 col-sm-10 col-xl-5 justify-center align-center d-flex flex-column pa-0 mt-3"
                >
                  <v-card-title> Enter your Life Expectancy. </v-card-title>
                  <v-card-subtitle> (80 Default) </v-card-subtitle>
                </v-card>
                <v-spacer></v-spacer>
                <v-card
                  elevation="5"
                  class="col-xs-10 col-sm-10 col-xl-5 justify-center align-center d-flex flex-column pa-0 mt-3 mb-3"
                >
                <v-card id="yearsCardTitle" class="ma-2 pb-5" color="#212121">
                  <v-card-title
                    class="d-flex mt-4 justify-center white--text"
                    style="font-size: 40px"
                  >
                    {{ formData.lifeExpectancy }} Years
                  </v-card-title>
                </v-card>
                  <v-divider></v-divider>
                  <v-card-text>
                    <v-slider
                      v-model="formData.lifeExpectancy"
                      height="150"
                      step="5"
                      min="60"
                      thumb-label
                      ticks
                      class="d-flex justify-center rounded-lg mt-3"
                    ></v-slider>
                    <v-card-subtitle class="d-flex justify-center"
                      >Use the slider above</v-card-subtitle
                    >
                  </v-card-text>
                </v-card>
                <v-spacer></v-spacer>
              </v-card>
              <div class="d-flex justify-center">
                <v-btn
                  color="#C68F55"
                  class="ma-5"
                  @click="
                    switchComponent();
                    $emit('handleSubmit', formData);
                  "
                >
                  Continue
                </v-btn>
                <v-btn text class="ma-5" @click="e1 = 1"> Go Back </v-btn>
              </div>
            </v-stepper-content>
          </v-stepper-items>
        </v-stepper>
        <v-spacer></v-spacer>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "enterData",
  data: () => {
    return {
      picker: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
      e1: 1,
      formData: {
        birthDate: "",
        lifeExpectancy: 80,
      },
      backgroundImage:
        "https://i.imgur.com/zKFw6sW.png",
    };
  },
  props: ["switch-component"],
  computed: {
    dateIsValid() {
      if (this.formData.birthDate == "") {
        return true;
      } else {
        return this.formData.birthDate >= this.picker;
      }
    },
  },
};
</script>

<style>
* {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
.rt-cards {
  word-break: normal;
  max-width: 100%;
}

.font-style {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

.enterDataCard {
  background-size: cover;
}

#enterDataIntro {
  font-size: 15px !important;
  color: 212121;
}

.backgroundColor {
  background-color: white;
}

#yearsCardTitle{
  border-radius: 10px 10px 0px 0px;
  width: 95%;
}

.e2-card {
  width: 100%;
}
</style>
