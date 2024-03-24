<script setup>
import { ref, defineEmits, defineProps } from 'vue' //declare reactive state

const props = defineProps({
  metricUnitsChecked: Boolean
})

//prepare variables to be defined by what Boolean says
let heightLabel = ''
let weightLabel = ''

function displayedLabels(metricUnitsChecked) { //if using American units (checkbox not checked), use these labels
  if(props.metricUnitsChecked === true) { //if using American units (checkbox not checked), use these labels
    heightLabel = 'Height in meters'
    weightLabel = 'Weight in kilograms'
  } else {
    heightLabel = 'Height in inches'
    weightLabel = 'Weight in pounds'
  }
}

displayedLabels(props.metricUnitsChecked)


//Create two reactive data and use v-model to connect with the form.
 const heightEntered = ref('')
 const weightEntered = ref('')


  //know data to expect to emit
const emit = defineEmits([
      'stats-entered'
  ])


function statsEntered() {
  //emit event to tell parent that user has made choice
  emit('stats-entered',  heightEntered.value, weightEntered.value )
  //height and weight values will be included in 'stats-entered' event when it is submitted
}
// When the user clicks the 'Calculate' button, BodyMassIndexForm should
// emit an event called stats-entered to App.vue with
// the user's height and the user's weight - this is the data the user entered in the form.
// use a function to emit event


</script>

<template>
  <div id="enterHeightWeight"> <!-- Show a form for the user to enter their height in meters, and weight in kilograms.  -->
    <h2>Enter your height and weight</h2>


    <label for="heightEntered" id="numberBox"> {{ heightLabel }} </label>
    <input v-model="heightEntered" id="heightEntered" >  <!-- use v-model to connect with the form.  -->


    <label for="weightEntered" id="numberBox"> {{  weightLabel }}  </label>
    <input v-model="weightEntered" id="weightEntered" >  <!-- use v-model to connect with the form.  -->


    <button v-on:click="statsEntered" type="button" id="button">Calculate</button>  <!-- Show a button with the text 'Calculate'   -->

  </div>
</template>

<style scoped>
  #enterHeightWeight {
    border: solid 3px darkred;
    padding: 20px;
    font-family: "Lucida Sans Typewriter"
  }


  #numberBox {
    margin: 1px 1px 1px 135px;


  }

  #button {
    background-color: darkgreen;
    border: solid 4px rosybrown;
    color: rosybrown;
    margin: 10px;
    font-size: 20px;
    font-family: "Lucida Sans Typewriter"
  }
</style>
