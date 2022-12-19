<template>
  <v-container class="grey darken-4 fill-height" fluid>
    <v-row>
      <v-col cols="9">
        <v-card height="fill" class="rounded-lg pa-5 overflow-y-auto">
          <v-icon small :key="n" v-for="n in weekCalculator"
            >mdi-checkbox-blank
          </v-icon>
          <v-icon small :key="n" v-for="n in weeksRemaining"
            >mdi-checkbox-blank-outline
          </v-icon>
        </v-card>
      </v-col>
      <v-col cols="3">
        <v-card class="rounded-lg">
          <v-card-title class="text-h6 text-wrap rt-cards"
            >Age: {{ ageCalculator }}</v-card-title
          >
        </v-card>
        <v-card class="rounded-lg mt-5 mb-5">
          <v-card-title class="text-h6 rt-cards"
            >Age in weeks: You have lived
            {{ weekCalculator }} weeks.</v-card-title
          >
        </v-card>
        <v-card class="rounded-lg mt-5 mb-5">
          <v-card-title class="text-h5 rt-cards"
            >Predicted Lifespan: {{ this.lifeExpectancy }} Years</v-card-title
          >
        </v-card>
        <v-card class="rounded-lg">
          <v-card-title class="text-h5 rt-cards"
            >Weeks Remaining: {{ weeksRemaining }} weeks</v-card-title
          >
        </v-card>
        <v-card>
          <v-card-title class="text-h5 rt-cards mt-5"
            >You have already lived {{ getPercentage }}% of your life.
          </v-card-title>
        </v-card>
        <v-btn class="justify-center py-4" @click="switchComponent()">Try Again</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "displayComponent",
  data: () => ({
  }),
  computed: {
    ageCalculator() {
      let today = new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10);
      let todayDay = Number(today.substr(8, 9));
      let todayMonth = Number(today.substr(5, 2));
      let todayYear = Number(today.substr(0, 4));
      let birthDay = Number(this.birthDate.substr(8, 9));
      let birthMonth = Number(this.birthDate.substr(5, 2));
      let birthYear = Number(this.birthDate.substr(0, 4));
      let years;
      let months;
      let days;
      if (this.birthDate == today) {
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
      let birthDay = Number(this.birthDate.substr(8, 9));
      let birthMonth = Number(this.birthDate.substr(5, 2));
      let birthYear = Number(this.birthDate.substr(0, 4));
      if (this.birthDate == today) {
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
      if (this.birthDate == today) {
        return "___";
      }
      return Math.floor(this.lifeExpectancy * 52.1775 - this.weekCalculator);
    },
    getPercentage() {
      let today = new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10);
      if (this.birthDate == today) {
        return "___";
      } else {
        let weeksLived = this.weekCalculator;
        let totalLife = this.lifeExpectancy * 52.1775;
        return Math.floor((weeksLived / totalLife) * 100);
      }
    },
  },
  props: ["switch-component", 'birthDate', 'lifeExpectancy'],
};
</script>

<style>
.rt-cards {
  word-break: normal;
  max-width: 100%;
}


</style>
