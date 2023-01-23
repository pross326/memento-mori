<template>
  <div>
      <component
      @handleSubmit="getFormData"
        :is="currentComponent"
        :switch-component="switchComponent"
        :birthDate="birthDate"
        :lifeExpectancy="lifeExpectancy"
      ></component>
      <footerComponent/>
  </div>
</template>

<script>
import displayComponent from "./displayComponent.vue";
import enterData from "./enterData.vue";
import footerComponent from './footerComponent.vue'

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
  components: { displayComponent, enterData, footerComponent },
};
</script>

<style>

*{
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif
}
</style>
