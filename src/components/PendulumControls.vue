// src/components/PendulumControls.vue
<template>
  <div class="pendulum-controls">
    <h3>Pendulum Settings</h3>
    <div
      v-for="(pendulum, index) in pendulums"
      :key="index"
      class="pendulum-item"
    >
      <label
        >Axis:
        <select v-model="pendulum.axis" @change="updatePendulums">
          <option value="x">X</option>
          <option value="y">Y</option>
        </select>
      </label>
      <label
        >Amplitude:
        <input
          type="number"
          v-model.number="pendulum.amplitude"
          step="0.1"
          @input="updatePendulums"
        />
      </label>
      <label
        >Frequency:
        <input
          type="number"
          v-model.number="pendulum.frequency"
          step="0.1"
          @input="updatePendulums"
        />
      </label>
      <label
        >Phase:
        <input
          type="number"
          v-model.number="pendulum.phase"
          step="0.1"
          @input="updatePendulums"
        />
      </label>
      <label
        >Damping:
        <input
          type="number"
          v-model.number="pendulum.damping"
          step="0.01"
          @input="updatePendulums"
        />
      </label>
      <button @click="removePendulum(index)">Remove</button>
    </div>
    <button @click="addPendulum">Add Pendulum</button>
  </div>
</template>

<script>
  import { ref, watch, onMounted } from "vue";

  export default {
    name: "PendulumControls",
    props: {
      modelValue: {
        type: Array,
        required: true,
      },
    },
    emits: ["update:modelValue"],
    setup(props, { emit }) {
      const pendulums = ref([]);

      const initializePendulums = () => {
        pendulums.value = JSON.parse(JSON.stringify(props.modelValue));
      };

      const updatePendulums = () => {
        emit("update:modelValue", JSON.parse(JSON.stringify(pendulums.value)));
      };

      const addPendulum = () => {
        pendulums.value.push({
          axis: "x",
          amplitude: 1,
          frequency: 1,
          phase: 0,
          damping: 0.1,
        });
        updatePendulums();
      };

      const removePendulum = (index) => {
        pendulums.value.splice(index, 1);
        updatePendulums();
      };

      watch(
        () => props.modelValue,
        (newValue) => {
          if (JSON.stringify(newValue) !== JSON.stringify(pendulums.value)) {
            initializePendulums();
          }
        },
        { deep: true }
      );

      onMounted(() => {
        initializePendulums();
      });

      return {
        pendulums,
        updatePendulums,
        addPendulum,
        removePendulum,
      };
    },
  };
</script>

<style scoped>
  .pendulum-controls {
    margin-bottom: 20px;
  }

  .pendulum-item {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  label {
    display: inline-block;
    margin-right: 10px;
    margin-bottom: 5px;
  }

  input,
  select {
    width: 60px;
    padding: 2px 5px;
  }

  button {
    margin-top: 10px;
    padding: 5px 10px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
  }

  button:hover {
    background-color: #45a049;
  }

  .pendulum-item button {
    background-color: #f44336;
  }

  .pendulum-item button:hover {
    background-color: #d32f2f;
  }
</style>
