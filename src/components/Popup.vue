<script setup>
import { Teleport, Transition } from "vue";

const { show, msg } = defineProps({ show: Boolean, msg: String });
</script>

<template>
  <Teleport to="body">
    <Transition>
      <div
        v-if="show"
        class="absolute bottom-6 bg-white text-black p-3 rounded w-96 transition-all"
      >
        <p class="text-center">{{ msg }}</p>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
/* we will explain what these classes do next! */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
