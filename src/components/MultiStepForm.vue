<script setup>
import { ref } from "vue";
import FormNav from "./FormNav.vue";

const currentStep = ref(1)

</script>

<template>
  <section
    class="md:flex w-screen md:h-screen items-center justify-center bg-magnolia"
  >
    <div
      class="md:w-[90%] lg:w-[80%] xl:w-[70%] md:bg-white-t rounded-xl md:shadow-md md:p-4 md:flex justify-center"
    >
      <div class="md:w-[30%] h-full">
        <FormNav></FormNav>
      </div>
      <div
        class="md:w-[70%] rounded-xl md:rounded-none bg-white-t md:px-10 lg:px-15 py-5 md:pt-10 -mt-20 md:-mt-0 mx-5 px-6"
        >
        <h1 class="text-3xl text-marine-blue ">Test Multi step Form</h1>
        <p class="mt-8"> Lorem ipsum dolor sit amet consectetur adipisicing elit.sunt voluptatibus 
            adipisci quia aliquam quisquam ab laboriosam,deleniti minima autem harum 
            libero dicta doloremque exercitationem ea numquam. Corrupti, facilis?
         </p>
    </div>
    </div>
  </section>
</template>
