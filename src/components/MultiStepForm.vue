<template>
  <section
    class="md:flex w-screen md:h-screen items-center justify-center bg-magnolia"
  >
    <div
      class="md:w-[90%] lg:w-[80%] xl:w-[70%] md:bg-white-t rounded-xl md:shadow-md md:p-4 md:flex justify-center"
    >
      <div class="md:w-[30%] h-full">
        <FormNav :steps="steps" :currentStep="currentStep"></FormNav>
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
            v-model="infosData"
            @isStepValid="responseValidationButton"
          ></StepInfos>

          <StepPlans
            v-if="currentStep === 2"
            v-model="planData"
            @isStepValid="responseValidationButton"
          ></StepPlans>

          <StepAddOns 
            v-if="currentStep === 3"
            v-model:selectedAddOns="selectedAddOns"
            :addOns="AddOns"
            :isYearlyPlan="planData.isYearlyPlan"
            ></StepAddOns>

          <StepSummary 
            v-if="currentStep === 4"
            @changePlan="changePlan"
            :addOns="selectedAddOnsDetails"
            :plan="planData"
          ></StepSummary>

          <div class="bg-white-t fixed md:static bottom-0 right-0 left-0">
            <FormFooter
              :disabledNext="!isNextValid"
              :disabledBack="currentStep === 1"
              @nextStep="nextStep"
              @goBack="backStep"
              :ComfirmButton="currentStep === steps.length"
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

console.log(steps.length);

const currentStep = ref(1);
const isNextValid = ref(false);
const isFinish = ref(false);

const infosData = ref({
  name: "",
  email: "",
  phoneNumber: "",
});

const planData = ref({
  selectedPlan: null,
  isYearlyPlan: false,
});

const responseValidationButton = (r) => {
  isNextValid.value = r;
};

const nextStep = () => {
  if (currentStep.value < steps.length) {
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


// ############# ADDONS #####################

const selectedAddOns = ref([])
const AddOns = [
  {
    id: 1,
    label: "Online service",
    description: "Access to multiplayer games",
    price: 1,
  },
  {
    id: 2,
    label: "Larger storage",
    description: "Extra 1TB of cloud save",
    price: 2,
  },
  {
    id: 3,
    label: "Customizable Profile",
    description: "Custom theme on your profile",
    price: 2,
  },
];

// ############# SUMMARY #####################
const changePlan = () => {
  currentStep.value = 2
}

const selectedAddOnsDetails = computed(() =>
    AddOns.filter(addOn => selectedAddOns.value.includes(addOn.id))
)

</script>
