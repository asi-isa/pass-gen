<script setup>
import { ref, watchEffect } from "vue";

const props = defineProps(["password", "options"]);

// 0 = Too Weak, 1 = Weak, 2 = Medium, 3 = Strong
const passwordStrength = ref(0);

function evaluatePassword() {
  const passwordLength = props.password.length;
  const numOptions = props.options.length;

  if (passwordLength > 16 && numOptions > 3) {
    return 3;
  }

  if (passwordLength > 12 && numOptions > 2) {
    return 2;
  }

  if (passwordLength > 10 && numOptions > 1) {
    return 1;
  }

  return 0;
}

watchEffect(() => {
  passwordStrength.value = evaluatePassword();
});
</script>

<template>
  <div class="flex justify-between bg-[#18171F] p-2 rounded-sm">
    <p class="strength">STRENGTH</p>

    <div class="flex gap-1">
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordStrength > -1 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordStrength > 0 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordStrength > 1 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordStrength > 2 }"
      ></div>
    </div>
  </div>
</template>

<style scoped></style>
