<script setup lang="ts">
import { ref } from "vue";

type InputTextProps = {
  label: string;
};
const model = defineModel<string>();
defineProps<InputTextProps>();

const inputRef = ref<HTMLInputElement | null>(null);

const clearModel = () => {
  if (inputRef.value) {
    model.value = "";
    inputRef.value.focus();
  }
};
</script>

<template>
  <label class="flex flex-col gap-4">
    {{ label }}
    <div class="relative">
      <input
        ref="inputRef"
        class="w-full border-gray-400 border rounded-md h-10 px-4 hover:border-blue-400 invalid:border-red-500 focus:border-green-400 focus:outline-none"
        type="text"
        autocomplete="off"
        v-model="model"
      />
      <i
        class="absolute right-2 top-1/2 -translate-y-1/2 cursor-pointer"
        @click="clearModel"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="28"
          height="28"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
        >
          <line x1="18" y1="6" x2="6" y2="18"></line>
          <line x1="6" y1="6" x2="18" y2="18"></line>
        </svg>
      </i>
    </div>
  </label>
</template>
