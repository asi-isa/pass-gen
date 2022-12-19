<script setup>
import { computed } from "vue";
import { IconCheck } from "@iconify-prerendered/vue-mdi";

const { name, value, modelValue } = defineProps({
  name: String,
  value: String,
  modelValue: Array,
});

defineEmits(["update:modelValue"]);

const checked = computed(() => {
  return modelValue.includes(value);
});
</script>

<template>
  <div
    class="flex items-center gap-2 cursor-pointer"
    @click="$emit('update:modelValue', value)"
  >
    <div
      class="w-4 h-4 border border-[var(--accent)] rounded-sm flex items-center content-center transition-colors duration-500"
      :class="{ 'bg-[var(--accent)]': checked }"
    >
      <IconCheck v-if="checked" class="text-[var(--color-background)]" />
    </div>

    <p class="name">{{ name }}</p>
  </div>
</template>

<style scoped></style>
