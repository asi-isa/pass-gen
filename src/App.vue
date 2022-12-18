<script setup>
import { ref } from "vue";
import { IconContentCopy } from "@iconify-prerendered/vue-mdi";

import Slider from "./components/Slider.vue";
import Option from "./components/Option.vue";
import StrengthIndicator from "./components/StrengthIndicator.vue";

const password = ref("");
const passwordLength = ref(12);
const options = ref(["uppercase", "lowercase", "numbers"]);

function addOrRemoveOption(option) {
  const idx = options.value.indexOf(option);

  if (idx === -1) {
    options.value.push(option);
  } else {
    options.value.splice(idx, 1);
  }
}

function generatePassword() {
  const lower = "abcdefghijklmnopqrstuvwxyz".split("");
  const upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
  const numbers = "0123456789".split("");
  const symbols = ".,-_#!*+-(){}[]=?:;".split("");

  const alpha = [];

  if (options.value.includes("lowercase")) {
    alpha.push(...lower);
  }
  if (options.value.includes("uppercase")) {
    alpha.push(...upper);
  }
  if (options.value.includes("numbers")) {
    alpha.push(...numbers);
  }
  if (options.value.includes("symbols")) {
    alpha.push(...symbols);
  }

  const tempPassword = [];
  for (let i = 0; i < passwordLength.value; i++) {
    const randomIdx = Math.floor(Math.random() * alpha.length);

    tempPassword.push(alpha[randomIdx]);
  }

  password.value = tempPassword.join("");
}
</script>

<template>
  <div class="flex flex-col gap-4 items-center w-72">
    <p class="text-xl mb-3">Password Generator</p>

    <div
      class="bg-[#2f2d37] w-full h-12 flex items-center justify-between px-3 py-2 rounded"
    >
      <p class="max-w-[80%] overflow-hidden whitespace-nowrap text-ellipsis">
        {{ password }}
      </p>

      <IconContentCopy class="text-[#A5FFAF] text-xl" />
    </div>

    <div class="bg-[#2f2d37] w-full flex flex-col gap-4 px-3 py-2 rounded">
      <div class="flex justify-between items-center">
        <p class="">Character Length</p>

        <p class="text-2xl text-[#A5FFAF]">{{ passwordLength }}</p>
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

      <div
        class="bg-[#A5FFAF] text-black py-2 border border-[#a5ffaf] rounded hover:bg-[#2f2d37] hover:text-[#a5ffaf] active:bg-[#2f2d37] active:text-[#a5ffaf] focus:bg-[#2f2d37] focus:text-[#a5ffaf] cursor-pointer transition-colors duration-500"
        @click="generatePassword"
      >
        <p class="text-center">GENERATE</p>
      </div>
    </div>
  </div>
</template>
