<template>
  <div>

    <window-component :weekCalculator="weekCalculator" :weeksRemaining="weeksRemaining" :lifeExpectancy="lifeExpectancy"
      :ageCalculator="ageCalculator" :getPercentage="getPercentage" />

    <v-container class="grey darken-4 fill-height" fluid>
      <v-card class="col-md-10 mx-auto my-4">
        <v-card-text id="intro-text" class="text-center">
          The graphic below represents a user's life expectancy in weeks, using filled boxes to represent the weeks
          that have already passed and empty boxes to represent the weeks that are still to come. By looking at the
          number of filled
          and empty boxes, we can see how much time has already passed and how much is still ahead of us, based on our
          life expectancy.
          This visualization serves as a reminder to make the most of every day, as we never know when our time will run
          out. This allows us to visualize the concept of memento mori,
          a reminder to live each day as if it were our last.
        </v-card-text>
      </v-card>
      <v-row>
        <ChartComponent/>
      </v-row>
      <v-row>
        <v-spacer></v-spacer>
        <v-col class="col-md-8 col-lg-10">
          <v-card id="shareableCard" class="rounded-lg pa-4 max-char">
            <img src="../assets/filled-box.svg" :key="n" v-for="n in weekCalculator"/>
            <img src="../assets/empty-box.svg" :key="n" v-for="n in weeksRemaining"/>
          </v-card>
        </v-col>
        <v-spacer></v-spacer>
      </v-row>
      <v-btn class="mx-auto my-5" @click="switchComponent()">
        Try Again
      </v-btn>
    </v-container>
  </div>
</template>

<script>
import windowComponent from "./windowComponent.vue";
import ChartComponent from "./chartComponent.vue";

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
  methods: {
  },
  components: { windowComponent, ChartComponent },
};
</script>

<style>
* {
  font-family: 'Merriweather', serif;
}

.rt-cards {
  word-break: normal;
  max-width: 100%;
}

.max-char {
  max-width: 108;
}

#intro-text {
  font-size: large;
  font-weight: 600;
  font: 'Merriweather', serif;
  line-height: 1.8em;
}
</style>

<!--52:36 64:45-->
