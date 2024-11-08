<script setup lang="ts">
import { ref } from "vue";

// Reactive variable to store the active title
const activeTitle = ref<"particulier" | "professionnel">("particulier");
</script>

<template>
  <div class="toggle">
    <!-- Switched Background -->
    <div
      class="siwtched"
      :style="{
        transform:
          activeTitle === 'professionnel'
            ? 'translateX(100%)'
            : 'translateX(0)',
      }"
    ></div>

    <div class="buttons">
      <!-- Button for "particulier" -->
      <div :class="{ active: activeTitle === 'particulier' }">
        <button @click="activeTitle = 'particulier'">particulier</button>
      </div>
      <!-- Button for "professionnel" -->
      <div :class="{ active: activeTitle === 'professionnel' }">
        <button @click="activeTitle = 'professionnel'">professionnel</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.toggle {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: red;
  width: fit-content;
  margin: auto;
  padding: 1rem 2rem;
  border-radius: 30px;
}

.buttons {
  display: flex;
  gap: 1rem;
  align-items: center;
  position: relative;
  z-index: 1;
}

button {
  background: none;
  border: none;
  padding: 0.5rem 1rem;
  cursor: pointer;
  font-weight: bold;
  color: #000;
}

.active button {
  color: #fff;
}

.siwtched {
  position: absolute;
  top: 0;
  left: 0;
  width: 50%;
  height: 100%;
  background-color: #586c13;
  border-radius: 30px;
  transition: transform 0.3s ease-in-out;
  z-index: 0;
}
</style>
