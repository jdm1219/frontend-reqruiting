<script setup lang="ts">
import { ref } from "vue";
import InputText from "./InputText.vue";
const userId = ref("");
const name = ref("");
const organization = ref("");

const USER_ID_REGEX = /[^a-zA-Z0-9]/;
const SPECIAL_CHARACTERS_REGEX = /[\\/:*?"<>|]/;

const validateUserId = () => {
  if (!userId.value) {
    throw new Error("User ID는 필수값입니다.");
  }
  if (USER_ID_REGEX.test(userId.value)) {
    throw new Error("User ID는 알파벳과 숫자만 허용됩니다.");
  }
};

const validateName = () => {
  if (!name.value) {
    throw new Error("Name은 필수값입니다.");
  }
  if (SPECIAL_CHARACTERS_REGEX.test(name.value)) {
    throw new Error("Name은 \\/:*?\"<>|의 특수문자가 허용되지 않습니다.");
  }
};

const validateOrganization = () => {
  if (organization.value && SPECIAL_CHARACTERS_REGEX.test(organization.value)) {
    throw new Error("Organization은 \\/:*?\"<>|의 특수문자가 허용되지 않습니다.");
  }
};

const validateForm = () => {
  try {
    validateUserId();
    validateName();
    validateOrganization();
    return true;
  } catch (error) {
    if (error instanceof Error) {
      alert(error.message);
    }
    return false;
  }
};


const handleSubmit = () => {
  if(!validateForm()) {
    return;
  }
  alert(`User ID: ${userId.value}
Name: ${name.value}
Organization: ${organization.value}`);
};
</script>

<template>
  <form class="flex flex-col gap-4 py-4" @submit.prevent="handleSubmit">
    <InputText label="User ID" v-model="userId" />
    <InputText label="Name" v-model="name" />
    <InputText label="Organization" v-model="organization" />
    <button class="bg-blue-500 text-white px-4 py-2 rounded-md">Submit</button>
  </form>
</template>
