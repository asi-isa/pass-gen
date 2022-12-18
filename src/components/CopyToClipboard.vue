<script setup>
import { ref } from "vue";
import { IconContentCopy } from "@iconify-prerendered/vue-mdi";

import Popup from "./Popup.vue";

const { value } = defineProps({ value: String });

const copiedSuccessfully = ref(false);

async function copyToClipboard() {
  console.log("yes no maybe");
  await navigator.clipboard.writeText(value);

  copiedSuccessfully.value = true;
  setTimeout(() => {
    copiedSuccessfully.value = false;
  }, 3300);
}
</script>

<template>
  <IconContentCopy
    @click="copyToClipboard"
    class="text-[#A5FFAF] text-xl cursor-pointer"
  />
  <Popup :show="copiedSuccessfully" msg="Successfully copied to clipboard!" />
</template>
