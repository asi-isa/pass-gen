<script setup>
const { name, value } = defineProps({
  name: String,
  value: String,
  modelValue: Array,
});

defineEmits(["update:modelValue"]);
</script>

<template>
  <div class="flex gap-2">
    <input
      type="checkbox"
      :value="value"
      :checked="modelValue.includes(value)"
      @change="$emit('update:modelValue', $event.target.value)"
    />
    <p class="name">{{ name }}</p>
  </div>
</template>

<style scoped></style>
