<template>
  <section
    class="md:flex w-screen md:h-screen items-center justify-center bg-magnolia"
  >
    <div
      class="md:w-[90%] lg:w-[80%] xl:w-[70%] md:bg-white-t rounded-xl md:shadow-md md:p-4 md:flex justify-center"
    >
      <div class="md:w-[30%] h-full">
        <FormNav :currentStep="currentStep" ></FormNav>
      </div>
      <div
        class="md:w-[70%] rounded-xl md:rounded-none bg-white-t md:px-10 lg:px-15 py-5 md:pt-10 -mt-20 md:-mt-0 mx-5 px-6"
        >
         <div class="flex flex-col justify-between w-full h-full">
            <StepInfos
              v-if="currentStep === 1"
              v-model="infosData"
              @isStepValid="responseValidationButton"
          ></StepInfos>

          <div class=" bg-white-t fixed md:static bottom-0 right-0 left-0 ">
            <FormFooter
            :disabledNext="!isNextValid"
            :disabledBack="currentStep === 1"
            @nextStep="nextStep"
            @goBack="backStep"
            :ComfirmButton="currentStep === 4"
          ></FormFooter>
          </div>
         </div>
    </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";
import FormNav from "./FormNav.vue";
import StepInfos from "./step/StepInfos.vue";
import FormFooter from "./step/content/FormFooter.vue";

const currentStep = ref(1)
const isNextValid = ref(false)

const infosData = ref({
  name: "",
  email: "",
  phoneNumber: "",
});

const responseValidationButton = (r) => {
  isNextValid.value = r;
};

const nextStep = () => {
  currentStep.value++
};

const backStep = () => {
  currentStep.value--
};
</script>
