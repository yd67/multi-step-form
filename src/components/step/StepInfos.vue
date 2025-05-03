<template>
    <FormHead
      title="Personal info "
      subTitle="Please provide your name, email address, and phone number."
    >
    </FormHead>
  
    <div class="mb-5">
      <div class="flex justify-between mb-2 text-sm font-medium">
        <label class="text-marine-blue" for="name"> Name </label>
        <span v-if="errors.name" class="block text-end text-red-600">{{
          errors.name
        }}</span>
      </div>
  
      <input
        :class="[
          'border-1 rounded-xl p-3 w-full  border-light-gray ',
          errors.name
            ? 'border-red-600 outline-red-600'
            : 'outline-purplish-blue',
        ]"
        type="text"
        name="name"
        placeholder=" e.g. Stephen King"
        v-model="infos.name"
        @input="validateName"
      />
    </div>
    <div class="mb-5">
      <div class="flex justify-between mb-2 text-sm font-medium">
        <label class="text-marine-blue" for="email"> Email </label>
        <span v-if="errors.email" class="block text-end text-strawberry-red">{{
          errors.email
        }}</span>
      </div>
      <input
        :class="[
          'border-1 rounded-xl p-3 w-full border-light-gray',
          errors.email
            ? 'border-strawberry-red outline-strawberry-red '
            : 'outline-purplish-blue',
        ]"
        type="email"
        name="email"
        placeholder=" e.g. stephenking@lorem.com"
        v-model="infos.email"
        @input="validateEmail"
      />
    </div>
    <div class="mb-5">
      <div class="flex justify-between mb-2 text-sm font-medium">
        <label class="text-marine-blue" for="phoneNumber"> Phone </label>
        <span
          v-if="errors.phoneNumber"
          class="block text-end text-strawberry-red"
          >{{ errors.phoneNumber }}</span
        >
      </div>
      <input
        :class="[
          'border-1 rounded-xl p-3 w-full border-light-gray',
          errors.phoneNumber
            ? 'border-strawberry-red outline-strawberry-red'
            : 'outline-purplish-blue',
        ]"
        type="text"
        name="phoneNumber"
        placeholder=" e.g. +1 234 567 890"
        v-model="infos.phoneNumber"
        @input="validatePhoneNumber"
      />
    </div>
  </template>
  
  <script setup>
  import { computed, ref, watch } from "vue";
  import FormHead from "./content/FormHead.vue";
  
  const infos = defineModel({
    name: String,
    email: String,
    phoneNumber: String,
  });
  
  const errors = ref({
    name: "",
    email: "",
    phoneNumber: "",
  });
  
  const isValid = computed(() => {
    if (
      infos.value.name !== "" &&
      infos.value.email !== "" &&
      infos.value.phoneNumber !== "" &&
      errors.value.name === "" &&
      errors.value.email === "" &&
      errors.value.phoneNumber === ""
    ) {
      return true;
    } else {
      return false;
    }
  });
  
  const validateName = computed(() => {
    if (infos.value.name === "" || infos.value.name == null) {
      errors.value.name = "The name is required";
    } else {
      errors.value.name = "";
    }
  });
  
  const validateEmail = computed(() => {
    const regex = /\S+@\S+\.\S+/;
    if (!regex.test(infos.value.email)) {
      errors.value.email = "The email is not valide";
    } else {
      errors.value.email = "";
    }
  });
  
  const validatePhoneNumber = computed(() => {
    if (infos.value.phoneNumber === "" || infos.value.phoneNumber == null) {
      errors.value.phoneNumber = "The phone is required";
    } else {
      errors.value.phoneNumber = "";
    }
  });
  
  const emit = defineEmits(["isStepValid"]);
  watch(isValid, (newValue) => {
    emit("isStepValid", newValue);
  });
  </script>
  