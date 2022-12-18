<script setup>
const { passwordLength, options } = defineProps({
  passwordLength: Number,
  options: Array,
});
</script>

<template>
  <div class="flex justify-between bg-[#18171F] p-2 rounded-sm">
    <p class="strength">STRENGTH</p>

    <div class="flex gap-1">
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordLength > 12 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordLength > 16 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordLength > 20 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordLength > 24 }"
      ></div>
    </div>
  </div>
</template>

<style scoped></style>
