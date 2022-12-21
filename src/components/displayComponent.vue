<template>
  <div>
    
    <window-component
      :weekCalculator="weekCalculator"
      :weeksRemaining="weeksRemaining"
      :lifeExpectancy="lifeExpectancy"
      :ageCalculator="ageCalculator"
      :getPercentage="getPercentage"
    />
   
    <v-container class="grey darken-4 fill-height" fluid>
      <v-row>
        <v-spacer></v-spacer>
        <v-col class="col-md-8 col-lg-10">
          <v-card class="rounded-lg pa-4 max-char">
            <v-icon x-small :key="n" v-for="n in weekCalculator"
              >mdi-checkbox-blank
            </v-icon>
            <v-icon x-small :key="n" v-for="n in weeksRemaining"
              >mdi-checkbox-blank-outline
            </v-icon>
          </v-card>
        </v-col>
        <v-spacer></v-spacer>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import windowComponent from "./windowComponent.vue";

export default {
  name: "displayComponent",
  data: () => ({}),
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
      return `${years} years, ${months} months, and ${days} days`;
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
  props: ["switch-component", "birthDate", "lifeExpectancy"],
  components: { windowComponent },
};
</script>

<style>
.rt-cards {
  word-break: normal;
  max-width: 100%;
}

.max-char {
  max-width: 108;
}
</style>

<!--52:36 64:45-->
