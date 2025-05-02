<template>
    <div
      class="bg-[url('./../assets/images/bg-sidebar-mobile.svg')] md:bg-[url('./../assets/images/bg-sidebar-desktop.svg')] bg-cover bg-center bg-no-repeat md:h-[575px] h-[24vh] md:px-5 lg:px-10 lg:py-10 pt-10 md:rounded-lg"
    >
      <ol class="flex md:flex-col justify-center gap-2 md:gap-3">
        <li v-for="s in steps" :key="s.step" class="flex items-center gap-4 mb-4">
          <div
            :class="[
              'w-8 h-8 rounded-full text-marine-blue border-1 flex items-center justify-center',
              ,
              currentStep === s.step
                ? 'bg-pastel-blue border-pastel-blue'
                : 'border-white-t text-white-t',
            ]"
          >
            {{ s.step }}
          </div>
          <div v-if="isMobile === false">
            <p class="text-cool-gray text-sm uppercase">{{ s.label }}</p>
            <h4 class="text-white-t text-sm font-bold uppercase">
              {{ s.description }}
            </h4>
          </div>
        </li>
      </ol>
    </div>
  </template>
  
  <script setup>
  import { useIsMobile } from "@/composables/useIsMobile.vue";
  
  const props = defineProps({
    currentStep: Number,
  });
  
  const isMobile = useIsMobile().isMobile;
  const steps = [
    {
      step: 1,
      label: "Step 1",
      description: "Your info",
    },
    {
      step: 2,
      label: "Step 2",
      description: "Select plan",
    },
    {
      step: 3,
      label: "Step 3",
      description: " Add-ons",
    },
    {
      step: 4,
      label: "Step 4",
      description: "Summary",
    },
  ];
  </script>
  