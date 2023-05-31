<script setup lang="ts">
import timer from "@/components/timer.vue"
import {ref, onMounted } from "vue";

const newYears = "1 Jan 2024";
const RemainingDays = ref("")
const RemainingHours = ref("")
const RemainingMinutes = ref("")
const RemainingSeconds = ref("")

function countDown() {
  const newYearsDate: Date = new Date(newYears);
  const currentDate: Date = new Date();

  const totalSeconds = (newYearsDate.getTime()-currentDate.getTime())/1000;
  
  const days = Math.floor(totalSeconds/3600/24);
  const hours = Math.floor(totalSeconds/3600)%24;
  const minutes = Math.floor(totalSeconds/60)%60;
  const seconds = Math.floor(totalSeconds)%60; 
  
  RemainingDays.value = setTime(days);
  RemainingHours.value = setTime(hours);
  RemainingMinutes.value = setTime(minutes);
  RemainingSeconds.value = setTime(seconds);
  
}

function setTime(value: string){
  return value >= 10 ? value.toString() :`0${value}`
}
let timeInterval: ReturnType<typeof setInterval>;
onMounted (()=> {
  timeInterval = setInterval(countDown,1000)
})
</script>


<template>
  <div class="container">
    <div class="title">
      New Year Countdown 
    </div>
    <div class="timer">
      <timer :count="RemainingDays" label="Days"/>
      <timer :count="RemainingHours" label="Hours"/>
      <timer :count="RemainingMinutes" label="Minutes"/>
      <timer :count="RemainingSeconds" label="Seconds"/>
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Fira+Sans&family=Roboto+Slab&display=swap');
body{
  margin: 0;
  font-family: 'Fira Sans', sans-serif;
  font-family: 'Roboto Slab', serif;
}

.container {
  height: 100vh;
  background-image: url("@/assets/mountain-rock.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  color: #323c41;
}

.title {
  text-align: center;
  font-size: 5rem;
  font-weight: bold;
}
.timer{
  display: flex;
  align-items: center;
  justify-content:space-around;
}
</style>
