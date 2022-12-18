<script setup>
const { min, max } = defineProps({
  min: Number,
  max: Number,
  modelValue: Number,
});

defineEmits(["update:modelValue"]);
</script>

<template>
  <input
    type="range"
    :min="min"
    :max="max"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>

<style scoped></style>
