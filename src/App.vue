<script setup>
import BodyMassIndexForm from './components/BodyMassIndexForm.vue'

import { ref } from 'vue'

const bmiCalculated = ref('')
const heightInput = ref('')
const weightInput = ref('')
const metricUnitsChecked = ref(false)  //box not checked initially


function computeBmi( height, weight ) {  //arguments are the data provided in what was emitted from child
  //then use reactive data defined in app.vue (heightInput and weightInput)
  //and update reactive data with what user entered in child/what was emitted from child
  heightInput.value = height
  weightInput.value = weight

  let bmi //declare a global variable to be used, but can't be defined yet- waiting for data
  if (metricUnitsChecked.value === true) { //if the metric box is checked, then use this calculation
    bmi = weight / (height * height)  //To calculate the body mass index, assuming variables called height and weight,  const bmi = weight / ( height * height )
  } else { //if the box is not checked, use this calculation for bmi
    bmi = (weight / (height * height) * 730)
  }
  bmiCalculated.value = bmi.toFixed(2) //Display the calculated body mass index, formatted to 2 decimal places.
}
</script>

<template>
  <div id="app-component">

    <h1>Body Mass Index Calculator</h1>

    <label for="checkboxUnits">
        <input type="checkbox" v-model="metricUnitsChecked"> <!-- v-model connects checkbox to variable -->
        Use Metric Units
    </label>

    <BodyMassIndexForm
        v-bind:useMetric="metricUnitsChecked"
        v-on:stats-entered="computeBmi"
    ></BodyMassIndexForm>
    <!-- v-bind sets the boolean in the checkbox with the prop sent to child-->
    <!-- Receive the stats-entered event from BodyMassIndexForm, and use the data sent to calculate the user's body mass index  -->
    <!-- info after = is what we want to do. In this case we want to compute the BMI with the info emitted-->
    <!-- computeBmi is a function we define-->

    <h2>BMI is: {{ bmiCalculated }}</h2>
    <!-- Display the bmi -->

  </div>
</template>

<style scoped>

#app-component {
  border: solid 3px midnightblue;
  width: 650px;
  padding: 20px;
}

h1 {
  margin: 5px;
  font-family: Calibri;
  padding: 10px 1px 20px 1px;
}
</style>
