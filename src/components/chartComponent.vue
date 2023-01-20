<template>
  <div class="example">
    <apexcharts
      width="500"
      height="350"
      type="pie"
      :options="chartOptions"
      :series="series"
    ></apexcharts>
    <v-btn @click="testing()">press</v-btn>
  </div>
</template>

<script>
import VueApexCharts from "vue-apexcharts";

export default {
  name: "ChartComponent",
  components: {
    apexcharts: VueApexCharts,
  },
  data() {
    return {
      chartOptions: {
        labels: ["Weeks Lived", "Weeks Remaining"],
      },
      series: [20, 20],
    };
  },
  methods: {
    testing() {
        window.alert(this.weekCalculator)
        window.alert(this.weeksRemaining)
    }
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
  },
};
</script>
