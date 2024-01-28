<template>
  <div :class="$style.container">
    <div :class="$style.sum">
      {{ sum }}
    </div>
    <div :class="$style.buttonRow">
      <button v-for="count of counter" :key="count" :class="$style.add" @click="add(count)">
        {{ count }}
      </button>
    </div>
    <div :class="$style.buttonRow">
      <button :class="$style.reset" @click="reset">
        Reset
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onKeyStroke } from '@vueuse/core'

const counter = [1, 2, 3, 4, 5]
const sum = ref(0)

function add(count: number) {
  sum.value += count
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

.container {
  padding: 10px;
  font-family: Inter,sans-serif;
  font-weight: bold;
  height: 100vh;
}

.sum {
  width: 100%;
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  background-color: #235753;
  color: white;
  padding: 40px 0;
}

.buttonRow {
  margin: 20px 0;
  display: flex;
  flex-flow: row wrap;
  width: 100%;
  gap: 20px;
  justify-content: center;

  button {
    padding: 40px 0;
    flex-basis: calc(50% - 10px);
    flex-shrink: 0;
    font-size: 20px;
    border: 0;
  }
}

.add {
  background-color: #A9D8D8;
}

.reset {
  color: white;
  background-color: #cc0070;
}
</style>
