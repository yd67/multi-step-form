<template>
  <div class="flex justify-between p-6 md:p-0 b-0 md:mt-4">
    <button
      type="button"
      @click="$emit('goBack')"
      :disabled="disabledBack"
      :class="[
        'text-marine-blue text-sm',
        disabledBack ? 'invisible' : 'cursor-pointer',
      ]"
    >
      Go Back
    </button>

    <button
      v-if="ComfirmButton"
      @click="$emit('nextStep')"
      class="bg-purplish-blue cursor-pointer px-5 py-2 rounded-sm md:rounded-md text-white-t text-md"
    >
      Comfirm
    </button>

    <button
      v-else
      type="button"
      @click="$emit('nextStep')"
      :disabled="disabledNext"
      :class="[
        'px-5 py-2 rounded-sm md:rounded-md text-white-t text-md',
        disabledNext
          ? 'cursor-not-allowed bg-pastel-blue'
          : 'cursor-pointer bg-marine-blue',
      ]"
    >
      Next Step
    </button>
  </div>
</template>

<script setup>
defineEmits(["goBack", "nextStep"]);
defineProps({
  disabledBack: Boolean,
  disabledNext: Boolean,
  ComfirmButton: Boolean,
});
</script>
