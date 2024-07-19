// src/components/TimeSettings.vue
<template>
  <div class="time-settings">
    <h3>Time Settings</h3>
    <div>
      <label
        >Start: <input type="number" v-model.number="computedTimeData.start"
      /></label>
      <label
        >End: <input type="number" v-model.number="computedTimeData.end"
      /></label>
      <label
        >Steps: <input type="number" v-model.number="computedTimeData.steps"
      /></label>
    </div>
  </div>
</template>

<script>
  import { computed } from "vue";

  export default {
    name: "TimeSettings",
    props: {
      timeData: {
        type: Object,
        required: true,
      },
    },
    emits: ["update:timeData"],
    setup(props, { emit }) {
      const computedTimeData = computed({
        get: () => props.timeData,
        set: (value) => emit("update:timeData", value),
      });

      return {
        computedTimeData,
      };
    },
  };
</script>

<style scoped>
  .time-settings {
    margin-bottom: 20px;
  }

  label {
    margin-right: 10px;
  }

  input {
    width: 60px;
  }
</style>
