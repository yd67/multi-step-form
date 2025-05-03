<template>
    <div>
      <FormHead
        title="Select your plan"
        sub-title="You have the option of monthly or yearly billing."
      ></FormHead>
      <div class="flex flex-col md:flex-row gap-3 md:gap-5 mb-5 md:mb-6">
        <div
          v-for="p in plans"
          :key="p.id"
          @click="handlePlanSelect(p)"
          :class="[
            'flex md:flex-col w-full gap-4 p-4 rounded-lg border-1 cursor-pointer hover:border-purplish-blue',
            myModel.selectedPlan != null && myModel.selectedPlan.id === p.id
              ? 'border-purplish-blue'
              : 'border-light-gray',
          ]"
        >
          <div class="md:mb-6">
            <img :src="p.icon" :alt="'icon-' + p.name" />
          </div>
  
          <div class="">
            <p class="text-marine-blue text-lg font-bold">{{ p.name }}</p>
            <div v-if="!myModel.isYearlyPlan">
              <span class="block text-md text-cool-gray my-1"
                >${{ p.price }}/mo</span
              >
            </div>
            <div v-else="myModel.isYearlyPlan">
              <span class="block text-md text-cool-gray my-1">
                {{ p.price * 10 }}/yrs</span
              >
              <span class="block text-sm text-marine-blue"
                >2 months free</span
              >
            </div>
          </div>
        </div>
      </div>
  
      <div class="flex justify-center p-3 bg-magnolia rounded-lg">
        <div class="flex gap-5">
          <span
            :class="[
              'font-medium',
              !myModel.isYearlyPlan ? 'text-marine-blue' : 'text-cool-gray',
            ]"
          >
            Monthly
          </span>
          <button
            @click="toggleBilling()"
            class="relative cursor-pointer w-12 h-6 bg-marine-blue rounded-full transition-all duration-300 focus:outline-none"
          >
            <span
              :class="[
                'absolute top-0.5 left-0.5 w-5 h-5 bg-white rounded-full transition-transform duration-200',
                myModel.isYearlyPlan ? 'translate-x-6' : 'translate-x-0',
              ]"
            ></span>
          </button>
          <span
            :class="[
              'font-medium',
              myModel.isYearlyPlan ? 'text-marine-blue' : 'text-cool-gray',
            ]"
          >
            Yearly
          </span>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import FormHead from "./content/FormHead.vue";
  import { computed, onMounted, watch } from "vue";
  
  const plans = [
    {
      id: 1,
      name: "Arcade",
      price: 9,
      icon: new URL("@/assets/images/icon-arcade.svg", import.meta.url).href,
    },
    {
      id: 3,
      name: "Advanced",
      price: 12,
      icon: new URL("@/assets/images/icon-advanced.svg", import.meta.url).href,
    },
    {
      id: 4,
      name: "Pro",
      price: 15,
      icon: new URL("@/assets/images/icon-pro.svg", import.meta.url).href,
    },
  ];
  
  const myModel = defineModel({
    selectedPlan: Object,
    isYearlyPlan: Boolean,
  });
  
  function handlePlanSelect(plan) {
    myModel.value.selectedPlan = plan;
  }
  
  function toggleBilling() {
    myModel.value.isYearlyPlan = !myModel.value.isYearlyPlan;
  }
  
  const isValid = computed(() => myModel.value.selectedPlan != null ? true : false );
  
  const emit = defineEmits(["isStepValid"]);
  watch(isValid, (newValue) => {
    emit("isStepValid", newValue);
  });
  
  onMounted(() => {
    emit("isStepValid", isValid.value);
  });
  </script>
  