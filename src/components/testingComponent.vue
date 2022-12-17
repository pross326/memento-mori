<template>
  <div>
    <enterData />
    <displayData @pass-data="handleEvent($event)" :picker="this.picker"/>
  </div>
</template>

<script>
import enterData from "./enterData.vue";
import displayData from "./displayData.vue";

export default {
  name: "testingComponent",
  components: { enterData, displayData },
  data: () => ({
    //
  }),
}


</script>

<style></style>
