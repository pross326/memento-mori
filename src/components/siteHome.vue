<template>
  <v-container class="grey darken-4 fill-height" fluid>
    <v-row class="ma-8">
      <v-col cols="3">
        <v-card class="d-flex align-center rounded-lg flex-column pa-1">
          <v-card-title class="text-h4"> Choose your birthday. </v-card-title>
          <v-date-picker
            full-width
            @input="picker"
            v-model="picker"
          ></v-date-picker>
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
            <v-card-subtitle class="text-h6 d-flex justify-center"
              >{{ this.value }} Years</v-card-subtitle
            >
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="6">
        <v-card class="fill-height rounded-lg"> testing </v-card>
      </v-col>
      <v-col cols="3">
        <v-card class="rounded-lg">
          <v-card-title class="text-h5">Age: {{ ageCalculator }}</v-card-title>
        </v-card>
        <v-card class="rounded-lg mt-5 mb-5">
          <v-card-title class="text-h5"
            >Age in weeks: You have lived {{ weekCalculator }} weeks</v-card-title
          >
        </v-card>
        <v-card class="rounded-lg mt-5 mb-5">
          <v-card-title class="text-h5"
            >Predicted Lifespan: {{ this.value }} Years</v-card-title
          >
        </v-card>
        <v-card class="rounded-lg">
          <v-card-title class="text-h5"
            >Weeks Remaining: {{ weeksRemaining }} weeks</v-card-title
          >
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
  computed: {
    ageCalculator() {
      let today = new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10);
      let todayDay = Number(today.substr(8, 9));
      let todayMonth = Number(today.substr(5, 2));
      let todayYear = Number(today.substr(0, 4));
      let birthDay = Number(this.picker.substr(8, 9));
      let birthMonth = Number(this.picker.substr(5, 2));
      let birthYear = Number(this.picker.substr(0, 4));
      let years;
      let months;
      let days;
      if (this.picker == today) {
        return "Enter your birthday to calculate your age.";
      }
      if (
        todayMonth > birthMonth ||
        (todayMonth == birthMonth && todayDay >= birthDay)
      ) {
        years = todayYear - birthYear;
      } else {
        years = todayYear - birthYear - 1;
      }
      if (todayDay >= birthDay) {
        months = todayMonth - birthMonth;
      } else if (todayDay - birthDay) {
        months = todayMonth - birthMonth - 1;
      }
      months = months < 0 ? months + 12 : months;
      let monthDays = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
      if (todayDay >= birthDay) {
        days = todayDay - birthDay;
      } else {
        days = todayDay - birthDay + monthDays[birthMonth];
      }
      return `You are ${years} years, ${months} months, and ${days} days old`;
    },

    weekCalculator(dt1, dt2) {
      let today = new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10);
      let todayDay = Number(today.substr(8, 9));
      let todayMonth = Number(today.substr(5, 2));
      let todayYear = Number(today.substr(0, 4));
      let birthDay = Number(this.picker.substr(8, 9));
      let birthMonth = Number(this.picker.substr(5, 2));
      let birthYear = Number(this.picker.substr(0, 4));
      if (this.picker == today) {
        return "___";
      } else {
        dt1 = new Date(birthYear, birthMonth, birthDay);
        dt2 = new Date(todayYear, todayMonth, todayDay);
        var diff = (dt2.getTime() - dt1.getTime()) / 1000;
        diff /= 60 * 60 * 24 * 7;
        let weeksOld = Math.abs(Math.round(diff));
        return weeksOld;
      }
    },
    weeksRemaining() {
      let today = new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10);
      if (this.picker == today) {
        return "___";
      }
      return Math.floor(this.value * 52.1775 - this.weekCalculator);
    },
  },
  methods: {},
};
</script>

<style></style>
