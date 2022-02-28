<script setup lang="ts">
import { ref, computed } from 'vue'

const totalSeconds = ref(0)
const running = ref(false)
const seconds = computed(() => {
  return totalSeconds.value % 60
})
const minutes = computed(() => {
  return Math.floor(totalSeconds.value / 60) - (60 * hours.value)
})
const hours = computed(() => {
  return Math.floor(totalSeconds.value / (60 * 60))
})

function prettifyNumber(number: number) {
  return `${number < 10 ? 0 : ''}${number}`
}

const prettySeconds = computed(() => prettifyNumber(seconds.value))
const prettyMinutes = computed(() => prettifyNumber(minutes.value))
const prettyHours = computed(() => prettifyNumber(hours.value))


function counterLoop() {
  if (!counter) {
    return setInterval(() => {
      totalSeconds.value += 1
    }, 1000)
  }
  return counter
}

let counter: number | null

function startCounter() {
  running.value = true
  counter = counterLoop()
}

function endCounter() {
  running.value = false
  if (counter) {
    clearInterval(counter)
  }
  counter = 0
}

function reset() {
  running.value = false
  if (counter) endCounter()
  totalSeconds.value = 0
}

</script>

<template>
  <h1> Counter </h1>

  <h3> {{ prettyHours }}:{{ prettyMinutes }}:{{ prettySeconds }} </h3>

  <button type="button" class="start" @click="startCounter" v-if="!running">start</button>
  <button type="button" class="end" @click="endCounter" v-if="running">end</button>
  <button type="button" class="reset" @click="reset">reset</button>

</template>

<style scoped>
button {
  border: none;
  border-radius: 10px;
  width: 150px;
  height: 40px;
  margin-right: 10px;
  font-size: large;
}

.start {
  background-color: #42b983;
}

.end {
  background-color: orange;
}

.reset {
  background-color: #eee;
}

a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
