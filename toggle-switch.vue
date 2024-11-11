<script setup lang="ts">
import { ref, watch, defineProps, defineEmits } from "vue";

const props = defineProps<{
  name: string;
  modelValue: boolean;
}>();

const emit = defineEmits<{
  (event: "update:modelValue", value: boolean): void;
}>();

// Create a local ref for isChecked and synchronize it with modelValue
const isChecked = ref(props.modelValue);

// Watch for changes in modelValue from the parent
watch(
  () => props.modelValue,
  (newValue) => {
    isChecked.value = newValue;
  }
);

// Emit the updated value when toggled
watch(isChecked, (newVal) => {
  emit("update:modelValue", newVal);
});
</script>

<template>
  <div class="toggle-container">
    <input
      type="checkbox"
      :id="name"
      :name="name"
      v-model="isChecked"
      class="toggle-checkbox"
    />
    <label :for="name" class="toggle-label">
      <span class="toggle-circle"></span>
    </label>
  </div>
</template>

<style scoped>
.toggle-container {
  display: flex;
  align-items: center;
}

.toggle-checkbox {
  opacity: 0;
  position: absolute;
}

.toggle-label {
  position: relative;
  width: 50px;
  height: 30px;
  background-color: #ccc;
  border-radius: 30px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.toggle-circle {
  position: absolute;
  top: 3px;
  left: 3px;
  width: 24px;
  height: 24px;
  background-color: white;
  border-radius: 50%;
  transition: transform 0.3s ease;
}

.toggle-checkbox:checked + .toggle-label {
  background-color: var(--vt-c-purple);
}

.toggle-checkbox:checked + .toggle-label .toggle-circle {
  transform: translateX(20px);
}
</style>
