<template>
  <v-col class="col-md-10">
  <v-card class="rounded-lg" tile>
    <v-window class="grey" v-model="currentSlide" vertical dark>
      <v-window-item v-for="window in windowItems" :key="window">
        <v-card
          color="grey"
          height="250"
          class="align-center d-flex flex-column pt-3 window-background text-center"
          v-bind:style="{ 'background-image': `url(${backgroundImage})` }"
        >
          <h1 class="align-center d-flex flex-column mt-5" style="color: white; font-size:larger">
            {{ window.title }}
          </h1>
          <v-card width="30%" class="pa-4 mt-4">
            <h1 class="align-center d-flex flex-column">{{ window.data }}</h1>
          </v-card>
        </v-card>
      </v-window-item>
      <v-window-item>
        <v-card
          color="grey"
          height="250"
          class="align-center d-flex justify-space-around pt-2 window-background"
          v-bind:style="{ 'background-image': `url(${backgroundImage})` }"
        >
          <v-card class="summary-card">
            <v-card-subtitle
              class="summary-card-title align-center d-flex flex-column pt-5 text-center"
            >
              You have been alive for
            </v-card-subtitle>
            <v-card-title class="summary-card-title align-center d-flex flex-column text-center">
              {{ this.ageCalculator }}
            </v-card-title>
          </v-card>

          <v-card class="summary-card">
            <v-card-subtitle
              class="summary-card-title align-center d-flex flex-column pt-5 text-center"
            >
              That's
            </v-card-subtitle>
            <v-card-title class="align-center d-flex flex-column">
              {{ this.weekCalculator.toLocaleString() }} weeks
            </v-card-title>
          </v-card>

          <v-card class="summary-card">
            <v-card-subtitle
              class="summary-card-title align-center d-flex flex-column pt-5 text-center"
            >
              If you were to live {{ this.lifeExpectancy }} years, you'd have
            </v-card-subtitle>
            <v-card-title class="align-center d-flex flex-column">
              {{ this.weeksRemaining.toLocaleString() }} weeks left
            </v-card-title>
          </v-card>

          <v-card class="summary-card">
            <v-card-subtitle
              class="summary-card-title align-center d-flex flex-column pt-5"
            >
              That means you've already lived
            </v-card-subtitle>
            <v-card-title class="align-center d-flex flex-column">
              {{ this.getPercentage }}% of your life
            </v-card-title>
          </v-card>
        </v-card>
      </v-window-item>
    </v-window>

    <v-card-actions @click="stopInterval" class="justify-space-between">
      <v-btn text @click="prev">
        <v-icon>mdi-chevron-left</v-icon>
      </v-btn>
      <v-item-group v-model="currentSlide" class="text-center" mandatory>
        <v-item
          v-for="n in length"
          :key="`btn-${n}`"
          v-slot="{ active, toggle }"
        >
          <v-btn :input-value="active" icon @click="toggle">
            <v-icon>mdi-record</v-icon>
          </v-btn>
        </v-item>
      </v-item-group>
      <v-btn text @click="next">
        <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
    </v-card-actions>
  </v-card>
</v-col>
</template>

<script>
export default {
  name: "windowComponent",
  data: () => {
    return {
      length: 5,
      currentSlide: 0,
      interval: null,
      backgroundImage: 'https://i.imgur.com/zKFw6sW.png'
    };
  },
  computed: {
    windowItems() {
      return [
        {
          title: "You have been alive for",
          data: this.ageCalculator,
        },
        {
          title: "That's",
          data: `${this.weekCalculator.toLocaleString()} weeks`,
        },
        {
          title: `If you were to live ${this.lifeExpectancy} years, you'd have`,
          data: `${this.weeksRemaining.toLocaleString()} weeks left`,
        },
        {
          title: `That means you've already lived`,
          data: `${this.getPercentage}% of your life.`,
        },
      ];
    },
  },
  mounted() {
    // Switch to the next slide every 5 seconds
    this.interval = setInterval(() => {
      this.currentSlide =
        (this.currentSlide + 1) % (this.windowItems.length + 1);
      if (this.currentSlide === 4) {
        clearInterval(this.interval); // stop the interval
        setTimeout(() => {
          // wait 10 seconds
          this.interval = setInterval(() => {
            // start the interval again
            this.currentSlide =
              (this.currentSlide + 1) % (this.windowItems.length + 1);
          }, 5000);
        }, 10000);
      }
    }, 5000);
  },

  methods: {
    next() {
      this.currentSlide =
        this.currentSlide + 1 === this.length ? 0 : this.currentSlide + 1;
    },
    prev() {
      this.currentSlide =
        this.currentSlide - 1 < 0 ? this.length - 1 : this.currentSlide - 1;
    },
    stopInterval() {
      clearInterval(this.interval);
      setTimeout(() => {
        setInterval(() => {
          this.currentSlide =
            (this.currentSlide + 1) % (this.windowItems.length + 1);
        }, 50000);
      }, 10000);
    },
  },
  props: {
    weekCalculator: {
      type: [String, Number],
      required: true,
    },
    weeksRemaining: {
      type: [String, Number],
      required: true,
    },
    lifeExpectancy: {
      type: [String, Number],
      required: true,
    },
    ageCalculator: {
      type: [Number],
      required: true,
    },
    getPercentage: {
      type: [Number],
      required: true,
    },
  },
};
</script>

<style>
.summary-card {
  height: 10em;
  width: 20em;
}

.summary-card-title{
  color: white;
  font-size: larger;
}

.window-background{
  background-size: cover;
}

</style>
