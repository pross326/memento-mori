<template>
  <div>
    <v-row class="justify-center pt-5 pb-3 grey darken-4 ">
      <v-card class="col-xs-10 col-sm-10 col-xl-8 justify-center align-center d-flex flex-column text-center pa-2 ma-2">
        <v-card-title class="text-h4 fw-bolder">
          Living a Life of Purpose and Gratitude
        </v-card-title>
        <v-card-text class="">
          Memento mori is a Latin phrase that means "remember that you have to
          die." It is a reminder to embrace the finite nature of life and to
          make the most of every moment. Memento mori serves as a reminder that we should focus on
          what truly matters in life, such as relationships, personal growth,
          and making a positive impact on the world. By embracing memento mori,
          we can live our lives with a sense of purpose, gratitude, and
          resilience, and make the most of every day.
        </v-card-text>
        <v-spacer></v-spacer>
        <v-card-text>
          Enter your birth date and life expectancy below for a visual reminder to live each day to the fullest. 
        </v-card-text>
      </v-card>
    </v-row>
    <v-container class="grey darken-4 " fluid height="fill">
      <v-row class="ma-1">
        <v-spacer></v-spacer>
        <v-stepper v-model="e1" class="col-md-8 col-xs-12">
          <v-stepper-header>
            <v-spacer></v-spacer>
            <v-stepper-step :complete="e1 > 1" step="1">
              Date of Birth
            </v-stepper-step>
            <v-divider></v-divider>
            <v-stepper-step :complete="e1 > 2" step="2">
              Life Expectancy
            </v-stepper-step>
            <v-spacer></v-spacer>
          </v-stepper-header>
          <v-stepper-items>
            <v-stepper-content step="1" class="align-items">
              <v-card height="fill" color="grey darken-2" class="d-flex flex-column align-center mb-5">
                <v-card elevation="4"
                  class=" col-xs-10 col-sm-10 col-xl-5 justify-center align-center d-flex flex-column pa-0 mt-3">
                  <v-card-title class="text-h5">
                    Enter your birth date.
                  </v-card-title>
                  <v-card-subtitle>
                    You birth date is used to calculate how many weeks you've
                    lived.
                  </v-card-subtitle>
                </v-card>
                  <v-date-picker elevation="4"
                    class="d-flex justify-center rounded-lg mb-3 mt-3 col-xs-10 col-sm-10 col-xl-5" @input="picker"
                    v-model="formData.birthDate"></v-date-picker>
              </v-card>
              <div class="d-flex justify-center">
                <v-btn :disabled="dateIsValid" color="primary" @click="e1 = 2">
                  Continue
                </v-btn>
              </div>
            </v-stepper-content>
            <v-stepper-content step="2" class="align-items">
              <v-card height="fill" color="grey darken-2" class="d-flex flex-column align-center mb-5">
                <v-card-title class="text-h4">
                  Enter your Life Expectancy.
                </v-card-title>
                <v-card-subtitle> (80 Default) </v-card-subtitle>
                </v-card>
                <v-card>
                  <v-spacer></v-spacer>
                  <v-col cols="8" class="justify-center mb-10">
                    <v-card elevation="5">
                      <v-card-title class="text-h2 d-flex justify-center">
                        {{ formData.lifeExpectancy }} Years
                      </v-card-title>
                      <v-card-text>
                        <v-slider v-model="formData.lifeExpectancy" height="150" step="10" min="60" thumb-label ticks
                          class="d-flex justify-center rounded-lg col-md-6 col-xl-8"></v-slider>
                        <v-card-subtitle class="d-flex justify-center">Use the slider above</v-card-subtitle>
                      </v-card-text>
                    </v-card>
                  </v-col>
                  <v-spacer></v-spacer>
                </v-card>
              <div class="d-flex justify-center">
                <v-btn color="primary" class="ma-5" @click="
                  switchComponent();
                $emit('handleSubmit', formData);
                ">
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
      steps: [
        {
          id: 1,
          title: 'Enter Your Birth Date',
          subtitle: "Your birth date is used to calculate how many weeks you've lived.",
          input: ''
        },
        {
          id: 2,
          title: 'Enter Your Life Expectancyt=',
          subtitle: "(80 Default)",
          input: ''
        }
      ],
      formData: {
        birthDate: "",
        lifeExpectancy: 80,
      },
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
.rt-cards {
  word-break: normal;
  max-width: 100%;
}

.e2-card {
  width: 100%;
}
</style>
