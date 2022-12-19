<template>
  <div>
    <transition name="fade">
      <component
      @handleSubmit="getFormData"
        :is="currentComponent"
        :switch-component="switchComponent"
        :birthDate="birthDate"
        :lifeExpectancy="lifeExpectancy"
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
      birthDate: '',
      lifeExpectancy: '',
    };
  },
  methods: {
    switchComponent() {
      this.currentComponent =
        this.currentComponent === "enterData"
          ? "displayComponent"
          : "enterData";
    },
    getFormData(formData){
      this.birthDate = formData.birthDate
      this.lifeExpectancy = formData.lifeExpectancy
    }
    
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
