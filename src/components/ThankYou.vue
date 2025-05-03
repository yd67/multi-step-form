<template>
    <div class="w-full h-full flex justify-center py-20 items-center">
      <div class="flex flex-col gap-4 text-center">
        <div class="flex justify-center">
          <img :src="icon" alt="thank-you-icon" />
        </div>
        <h2 class="text-2xl text-marine-blue font-bold">Thank you!</h2>
        <p class="text-md text-cool-gray">
          Thanks for confirming your subscription! We hope you have fun using our
          platform. If you ever need support, please feel free to email us at
          support@loremgaming.com.
        </p>
      </div>
    </div>
  </template>
  
  <script setup>
  import icon from "@/assets/images/icon-thank-you.svg";
  </script>
  