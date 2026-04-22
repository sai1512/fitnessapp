<script setup>
import Welcome from './components/pages/Welcome.vue'
import Layout from './components/layouts/Layout.vue'
import Dashboard from './components/pages/Dashboard.vue'
import Workout from './components/pages/Workout.vue';
import { ref, computed } from 'vue';
import { workoutProgram } from './utils';

const defaultData = {}
for(let workoutIdx in workoutProgram) {
  const workoutData = workoutProgram[workoutIdx]
  
  defaultData[workoutIdx] = {}
  for (let e of workoutData.workout) {
    defaultData[workoutIdx][e.name] = ''
  }
}


const selectedDisplay = ref(1);
const data = ref(defaultData);
const selectedWorkout = ref(-1);

const isWorkoutComplete = computed(() => {
  const currWorkout = data.value?.[selectedWorkout.value]
  if (!currWorkout) return false;

  const isCompleteCheck = Object.values(currWorkout).every(ex => !!ex)
  console.log('isCompleteCheck', isCompleteCheck);
  return isCompleteCheck;
})

const firstIncompleteWorkoutIndex = computed(() => {
  const allWorkouts = data.value
  for (const [index, workout] of Object.entries(allWorkouts)) {
    const isCompleteCheck = Object.values(workout).every(ex => !!ex)
    if (!isCompleteCheck) {
      return parseInt(index);
    }
  }
  return -1;
})

function handleChangeDisplay(idx) {
  selectedDisplay.value = idx;
}

function handleSelectWorkout(idx) {
  selectedWorkout.value = idx;
  selectedDisplay.value = 3;
}

function handleSaveWorkout() {
  localStorage.setItem('workoutData', JSON.stringify(data.value))
  //Show dashboard
  selectedDisplay.value = 2;
  // deselect workout
  selectedWorkout.value = -1;
}

</script>

<template>
  <Layout>
    <!-- Page 1 -->
    <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay == 1" />
    <!-- Page 2 -->
    <Dashboard :handleSelectWorkout="handleSelectWorkout" v-if="selectedDisplay == 2" />
    <!-- Page 3 -->
    <Workout :data="data" :selectedWorkout="selectedWorkout" v-if="selectedDisplay == 3 && workoutProgram?.[selectedWorkout]" />
  </Layout>
</template>

<style scoped>

</style>
