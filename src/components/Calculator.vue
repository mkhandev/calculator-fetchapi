<script setup>
import { ref } from "vue";

const num1 = ref(0);
const num2 = ref(0);
const operation = ref("+");
const result = ref(null);

const calculate = () => {
  switch (operation.value) {
    case "+":
      result.value = num1.value + num2.value;
      break;
    case "-":
      result.value = num1.value - num2.value;
      break;
    case "*":
      result.value = num1.value * num2.value;
      break;
    case "/":
      result.value = num1.value / num2.value;
      break;
    default:
      result.value = null;
  }
};
</script>

<template>
  <div class="w-[300px] mx-auto mt-8 p-6 bg-gray-100 rounded-lg shadow-md text-center">
    <div class="mb-4">
      <label for="num1" class="block text-gray-700 text-sm font-bold mb-2"
        >Number 1:</label
      >
      <input
        v-model="num1"
        type="number"
        id="num1"
        class="w-full border rounded-md py-2 px-3"
      />
    </div>
    <div class="mb-4">
      <label for="operation" class="block text-gray-700 text-sm font-bold mb-2"
        >Operation:</label
      >
      <select
        v-model="operation"
        id="operation"
        class="w-full border rounded-md py-2 px-3"
      >
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
      </select>
    </div>
    <div class="mb-4">
      <label for="num2" class="block text-gray-700 text-sm font-bold mb-2"
        >Number 2:</label
      >
      <input
        v-model="num2"
        type="number"
        id="num2"
        class="w-full border rounded-md py-2 px-3"
      />
    </div>
    <button
      @click="calculate"
      class="mx-auto bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600"
    >
      Calculate
    </button>
    <div v-if="result !== null" class="mt-4">
      <p class="text-lg font-bold">Result: {{ result }}</p>
    </div>
  </div>
</template>

<style></style>
