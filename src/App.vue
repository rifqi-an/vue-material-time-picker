<template>
  <div style="display: flex">
    <time-picker
      v-model="time"
      :disabled-hours="disabledHours"
      :disabled-minutes="disabledMinutes"
      :disabled-seconds="disabledSeconds"
      use-seconds
    >
    </time-picker>

    {{ time }}
  </div>
  <div style="display: flex">
    <button @click="hide">Hide</button>
    <button @click="setVal">Set val</button>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from "vue";
import timePicker from "./components/timePicker.vue";

const time = ref<Date | null | string>(null);
const hidden = ref(false);
const disabledHours = ref([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 23]);
const disabledMinutes = ref([]);
const disabledSeconds = ref([5, 10]);

const setVal = () => {
  time.value = "12:04:04";
};

const hide = () => {
  hidden.value = !hidden.value;
};

const changed = () => {
  console.log("bruh");
};

const generateDisabledMinutes = () => {
  const disabledMinutes = [];
  for (let i = 0; i < 60; i++) {
    if (i % 10 !== 0) {
      disabledMinutes.push(i);
    }
  }
  return disabledMinutes;
};

onMounted(() => {
  disabledMinutes.value = generateDisabledMinutes();
});
</script>
