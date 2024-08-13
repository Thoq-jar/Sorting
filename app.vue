<script lang="ts">
import { defineComponent, ref } from 'vue';

function Sort(arr: number[]): number[] {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[Math.floor(arr.length / 2)];
  const left = arr.filter(x => x < pivot);
  const right = arr.filter(x => x > pivot);
  const middle = arr.filter(x => x === pivot);

  return [...Sort(left), ...middle, ...Sort(right)];
}

export default defineComponent({
  setup() {
    const inputData = ref('');
    const outputData = ref('');

    const sortData = () => {
      const inputArray = inputData.value.split(',').map(Number);
      const sortedArray = Sort(inputArray);
      outputData.value = sortedArray.join(', ');
    };

    return {
      inputData,
      outputData,
      sortData
    };
  }
});
</script>

<template>
  <title>Sorting Demo</title>
  <div class="wrapper">
    <h1 class="title noselect">Sort Demo</h1>
    <h4>(Insert data separated with a ',' in between each number)</h4>
    <textarea v-model="inputData" class="input noselect blackandwhite" placeholder="Enter your data here..."></textarea>
    <button class="button noselect" @click="sortData">Sort</button>
    <textarea v-model="outputData" class="output blackandwhite" inputmode="none" placeholder="Output will show here..." disabled></textarea>
  </div>
</template>

<style lang="scss">
body {
  overflow: hidden;
  background: black;
  color: white;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
}

.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.noselect {
  user-select: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}

.blackandwhite {
  background: black;
  color: white;
}

.title {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.input {
  width: 25%;
  height: 10rem;
  margin-bottom: 1rem;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid white;
  font-size: 1rem;

  &:focus {
    outline: none;
  }
}

.button {
  padding: 0.5rem 1rem;
  font-size: 1.2rem;
  cursor: pointer;
  border-radius: 5px;
  color: white;
  background: black;
  border: 2px solid white;
  transition: all 300ms ease;
  box-shadow: #999 0 0 15px;

  &:hover {
    border-radius: 7px;
    box-shadow: white 0 0 25px;
    background: white;
    color: black;
  }
}

.output {
  width: 25%;
  height: 10rem;
  margin-top: 1rem;
  padding: 1rem;
  font-size: 1rem;
  border-radius: 8px;
  border: 1px solid white;
  cursor: default;

  &:focus {
    outline: none;
  }
}
</style>