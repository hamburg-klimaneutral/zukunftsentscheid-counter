<template>
  <table cellspacing="10">
    <tbody>
      <tr>
        <th colspan="2" :class="$style.sum">
          {{ sum }}
        </th>
      </tr>
      <tr>
        <td :class="$style.add" @click="add(1)">1</td>
        <td :class="$style.add" @click="add(2)">2</td>
      </tr>
      <tr>
        <td :class="$style.add" @click="add(3)">3</td>
        <td :class="$style.add" @click="add(4)">4</td>
      </tr>
      <tr>
        <td :class="$style.add" @click="add(5)" colspan="2">5</td>
      </tr>
      <tr>
        <td :class="$style.reset" @click="reset" colspan="2">Reset</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup lang="ts">
import { onKeyStroke, useLocalStorage } from '@vueuse/core'

const sum = useLocalStorage('sum', 0)

const GOAL = 100

function tryVibrate(pattern: VibratePattern) {
  try {
    navigator.vibrate(pattern)
  } catch(e) {
    console.debug('cannot vibrate')
  }
}

watch(sum, (value, oldValue) => {
  if(oldValue < GOAL && value >= GOAL) {
    console.log('GOAL REACHED')
    tryVibrate([200, 100, 200])
  }
})

const counter = [1, 2, 3, 4, 5]

function add(count: number) {
  sum.value += count
  tryVibrate([200])
}

function reset() {
  sum.value = 0
}

onKeyStroke(counter.map(number => number.toString()), (e) => {
  add(parseInt(e.key, 10))
  e.preventDefault()
})

</script>

<style module>

table {
  width: 100%;
  height: 100%;
  font-family: Inter, sans-serif;
  font-weight: bold;
  text-align: center;
}

.goalReached .sum {
  background-color: #cc0070;
}

.sum {
  font-size: 20px;
  background-color: #235753;
  color: white;
}

.add {
  background-color: #A9D8D8;
}

.reset {
  color: white;
  background-color: #cc0070;
}
</style>
