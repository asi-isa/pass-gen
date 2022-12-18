<script setup>
import { ref, watch } from "vue";
import { IconArrowRight, IconContentCopy } from "@iconify-prerendered/vue-mdi";

import Slider from "./components/Slider.vue";
import Option from "./components/Option.vue";
import StrengthIndicator from "./components/StrengthIndicator.vue";

const passwordLength = ref(12);
const options = ref(["lowercase"]);

function addOrRemoveOption(option) {
  const idx = options.value.indexOf(option);

  if (idx === -1) {
    options.value.push(option);
  } else {
    options.value.splice(idx, 1);
  }
}
</script>

<template>
  <div class="flex flex-col gap-4 items-center w-72">
    <p class="text-xl mb-3">Password Generator</p>

    <div
      class="bg-[#2f2d37] w-full flex items-center justify-between px-3 py-2 rounded"
    >
      <p class="password">some strong</p>

      <IconContentCopy class="text-green-400" />
    </div>

    <div class="bg-[#2f2d37] w-full flex flex-col gap-3 px-3 py-2 rounded">
      <div class="flex justify-between items-center">
        <p class="">Character Length</p>

        <p class="text-2xl text-green-400">{{ passwordLength }}</p>
      </div>

      <Slider min="7" max="33" v-model="passwordLength" />

      <div class="options-con">
        <Option
          name="Include Uppercase Letters"
          value="uppercase"
          :modelValue="options"
          @update:modelValue="addOrRemoveOption"
        />
        <Option
          name="Include Lowercase Letters"
          value="lowercase"
          :modelValue="options"
          @update:modelValue="addOrRemoveOption"
        />
        <Option
          name="Include Numbers"
          value="numbers"
          :modelValue="options"
          @update:modelValue="addOrRemoveOption"
        />
        <Option
          name="Include Symbols"
          value="symbols"
          :modelValue="options"
          @update:modelValue="addOrRemoveOption"
        />
      </div>

      <StrengthIndicator :passwordLength="passwordLength" :options="options" />

      <div class="btn-con">
        <p class="btn-text">GENERATE</p>

        <IconArrowRight />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
