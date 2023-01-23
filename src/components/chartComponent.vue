<template>
  <div>
    <v-card>
      <apexcharts
        id="shareableCard"
        width="500"
        height="250"
        type="donut"
        :options="chartOptions"
        :series="series"
      ></apexcharts>
      <div class="d-flex justify-end">
        <v-btn color="success" class="ma-4" @click="downloadCard()">Share</v-btn>
      </div>
    </v-card>
  </div>
</template>

<script>
import VueApexCharts from "vue-apexcharts";
import html2canvas from "html2canvas";

export default {
  name: "ChartComponent",
  components: {
    apexcharts: VueApexCharts,
  },
  data() {
    return {
      chartOptions: {
        labels: ["Weeks Lived", "Weeks Remaining"],
        colors: ["#000000", "#D3D3D3"],
      },
      series: [this.weekCalculator, this.weeksRemaining],
    };
  },
  methods: {
    testing() {
      window.alert(this.weeksRemaining);
    },
    downloadCard() {
      html2canvas(document.querySelector("#shareableCard")).then((canvas) => {
        // Get the canvas data as a png image
        let imgData = canvas.toDataURL("image/png");

        // Create a link element to trigger the download
        let link = document.createElement("a");
        link.download = "v-card.png";
        link.href = imgData;
        link.click();
      });
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
  },
};
</script>
