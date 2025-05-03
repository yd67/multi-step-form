<template>
  <section
    class="md:flex w-screen md:h-screen items-center justify-center bg-magnolia"
  >
    <div
      class="md:w-[90%] lg:w-[80%] xl:w-[70%] md:bg-white-t rounded-xl md:shadow-md md:p-4 md:flex justify-center"
    >
      <div class="md:w-[30%] h-full">
        <FormNav :steps="allSteps" :currentStep="currentStep"></FormNav>
      </div>
      <div
        class="md:w-[70%] rounded-xl md:rounded-none bg-white-t md:px-10 lg:px-15 py-5 md:pt-10 -mt-20 md:-mt-0 mx-5 px-6"
      >
        <div v-if="isFinish">
          <ThankYou></ThankYou>
        </div>
        <div v-else class="flex flex-col justify-between w-full h-full">
          <StepInfos
            v-if="currentStep === 1"
            v-model="formData.infos"
            @isStepValid="responseValidationButton"
          ></StepInfos>

          <StepPlans
            v-if="currentStep === 2"
            :plans="allPlans"
            v-model="formData.plan"
            @isStepValid="responseValidationButton"
          ></StepPlans>

          <StepAddOns
            v-if="currentStep === 3"
            v-model:selectedAddOns="formData.addOns"
            :addOns="allAddOns"
            :isYearlyPlan="formData.plan.isYearlyPlan"
          ></StepAddOns>

          <StepSummary
            v-if="currentStep === 4"
            @changePlan="changePlan"
            :addOns="selectedAddOnsDetails"
            :plan="formData.plan"
          ></StepSummary>

          <div class="bg-white-t fixed md:static bottom-0 right-0 left-0">
            <FormFooter
              :disabledNext="!isNextValid"
              :disabledBack="currentStep === 1"
              @nextStep="nextStep"
              @goBack="backStep"
              :ComfirmButton="currentStep === allSteps.length"
            ></FormFooter>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from "vue";
import FormNav from "./FormNav.vue";
import FormFooter from "./step/content/FormFooter.vue";
import StepInfos from "./step/StepInfos.vue";
import StepPlans from "./step/StepPlans.vue";
import StepAddOns from "./step/StepAddOns.vue";
import StepSummary from "./step/StepSummary.vue";
import ThankYou from "./ThankYou.vue";
import { allSteps, allPlans, allAddOns } from "@/data/data.vue";

const currentStep = ref(1);
const isNextValid = ref(false);
const isFinish = ref(false);

const formData = ref({
  infos: {
    name: "",
    email: "",
    phoneNumber: "",
  },
  plan: {
    selectedPlan: null,
    isYearlyPlan: false,
  },
  addOns: [],
});

const nextStep = () => {
  if (currentStep.value < allSteps.length) {
    currentStep.value++;
  } else {
    isFinish.value = true;
  }
};

const backStep = () => {
  if (currentStep.value > 1) {
    currentStep.value--;
  }
};

const responseValidationButton = (r) => {
  isNextValid.value = r;
};

const selectedAddOnsDetails = computed(() =>
  allAddOns.filter((addOn) => formData.value.addOns.includes(addOn.id))
);

const changePlan = () => {
  currentStep.value = 2;
};

</script>
