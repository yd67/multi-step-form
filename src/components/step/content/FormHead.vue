<template>
  <h2 class="text-marine-blue text-2xl md:text-3xl font-bold mb-2 mt-4">
    {{ title }}
  </h2>
  <p class="text-cool-gray text-sm mb-10">
    {{ subTitle }}
  </p>
</template>

<script setup>
defineProps({
  title: String,
  subTitle: String,
});
</script>
