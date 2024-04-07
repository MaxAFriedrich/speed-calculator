<script setup lang="ts">
import {ref} from 'vue';

import Speed from "@/components/icons/Speed.vue";
import Elivation from "@/components/icons/Elivation.vue";
import Distance from "@/components/icons/Distance.vue";
import Time from "@/components/icons/Time.vue";


const speed = ref(5);
const distance = ref(3);
const elevation = ref(100);
const hours = ref(0);
const minutes = ref(0);

function hoursToMinuets(rawHours: number) {
  hours.value = Math.floor(rawHours);
  minutes.value = Math.round((rawHours - hours.value) * 60);
}

function minuetsToHours() {
  return hours.value + minutes.value / 60;
}

function calculate() {
  const speedValue = speed.value;
  const distanceValue = distance.value;
  const elevationValue = elevation.value;
  const timeValue = minuetsToHours();

  const timeInSeconds = timeValue * 3600;
  const distanceInMeters = distanceValue * 1000;
  const timeInSecondsWithElevation = timeInSeconds + (elevationValue / 10);
  const speedInMetersPerSecond = speedValue / 3.6;

  const timeToCompleteWithElevation = distanceInMeters / speedInMetersPerSecond + timeInSecondsWithElevation;

  hoursToMinuets(timeToCompleteWithElevation / 3600);
}

calculate();
</script>

<template>
  <div class="property">
    <Speed/>
    <label for="speed">Speed (km/h)</label>
    <input type="number" id="speed" v-model="speed"/>
  </div>
  <div class="property">
    <Distance/>
    <label for="distance">Distance (km)</label>
    <input type="number" id="distance" v-model="distance"/>
  </div>
  <div class="property">
    <Elivation/>
    <label for="elevation">Elevation Gain (m)</label>
    <input type="number" id="elevation" v-model="elevation"/>
  </div>
  <div class="time">
    <div class="property">
      <Time/>
      <label>Time </label>
    </div>
    <div class="property">
      <label for="hours">Hours</label>
      <span>{{hours}}</span>
    </div>
    <div class="property">
      <label for="minutes">Minutes</label>
      <span>{{minutes}}</span>
    </div>
  </div>
</template>

<style scoped>

</style>
