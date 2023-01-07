<script setup>
import { ref, watchEffect } from "vue";
import { passwordStrength } from "check-password-strength";

const props = defineProps(["password"]);

// 0 = Too Weak, 1 = Weak, 2 = Medium, 3 = Strong
const passwordStrengthId = ref(0);

const passwordStrengthOptions = [
  {
    id: 0,
    value: "Too weak",
    minDiversity: 0,
    minLength: 0,
  },
  {
    id: 1,
    value: "Weak",
    minDiversity: 2,
    minLength: 8,
  },
  {
    id: 2,
    value: "Medium",
    minDiversity: 3,
    minLength: 13,
  },
  {
    id: 3,
    value: "Strong",
    minDiversity: 4,
    minLength: 18,
  },
];

watchEffect(() => {
  passwordStrengthId.value = passwordStrength(
    props.password,
    passwordStrengthOptions
  ).id;
});
</script>

<template>
  <div class="flex justify-between bg-[#18171F] p-2 rounded-sm">
    <p class="strength">STRENGTH</p>

    <div class="flex gap-1">
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordStrengthId > -1 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordStrengthId > 0 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordStrengthId > 1 }"
      ></div>
      <div
        class="w-2 border border-white transition-colors duration-700"
        :class="{ 'bg-white': passwordStrengthId > 2 }"
      ></div>
    </div>
  </div>
</template>

<style scoped></style>
