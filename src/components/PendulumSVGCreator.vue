// src/components/PendulumSVGCreator.vue
<template>
  <div class="pendulum-svg-creator">
    <PendulumControls v-model="data.pendulums" />
    <TimeSettings v-model:timeData="data.time" />
    <div class="svg-container">
      <!-- SVG will be inserted here -->
    </div>
  </div>
</template>

<script>
  import { ref, onMounted } from "vue";
  import PendulumControls from "./PendulumControls.vue";
  import TimeSettings from "./TimeSettings.vue";

  export default {
    name: "PendulumSVGCreator",
    components: {
      PendulumControls,
      TimeSettings,
    },
    setup() {
      const data = ref({
        time: { start: 0, end: 100, steps: 1000 },
        pendulums: [],
      });

      onMounted(async () => {
        try {
          const response = await fetch("/data.json");
          const jsonData = await response.json();
          data.value = {
            ...data.value,
            ...jsonData,
          };
          console.log("Loaded data:", data.value);
        } catch (error) {
          console.error("Error loading data.json:", error);
        }
      });

      return {
        data,
      };
    },
  };
</script>

<style scoped>
  .pendulum-svg-creator {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .svg-container {
    width: 500px;
    height: 500px;
    border: 1px solid #ccc;
    margin-top: 20px;
  }
</style>
