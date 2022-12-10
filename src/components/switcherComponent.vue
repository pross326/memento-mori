<template>
  <div>
    <transition name="fade">
      <component
        :is="currentComponent"
        :switch-component="switchComponent"
      ></component>
    </transition>
  </div>
</template>

<script>
import displayComponent from "./displayComponent.vue";
import enterData from "./enterData.vue";

export default {
  name: "switcherComponent",
  data() {
    return {
      currentComponent: "enterData",
    };
  },
  methods: {
    switchComponent() {
      this.currentComponent =
        this.currentComponent === "enterData"
          ? "displayComponent"
          : "enterData";
    },
  },
  components: { displayComponent, enterData },
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: all 0.8s ease-in-out;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
