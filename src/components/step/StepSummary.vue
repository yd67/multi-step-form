<template>
  <FormHead
    title="Finishing up"
    sub-title="Double-check everything looks OK before confirming."
  ></FormHead>
  <div class="rounded-lg bg-magnolia p-6">
    <div class="flex justify-between">
      <div class="">
        <span class="block text-marine-blue font-bold">
          {{ plan.selectedPlan.name }} {{ longSuffix }}
        </span>
        <span
          @click="$emit('changePlan')"
          class="text-sm text-cool-gray hover:text-purplish-blue cursor-pointer"
          >Change</span
        >
      </div>
      <div class="block text-marine-blue font-bold">
        {{ planPrice }} {{ smallSuffix }}
      </div>
    </div>
    <hr class="my-4 border-1 border-light-gray" />
    <div class="flex justify-between" v-for="a in addOns">
      <span class="block text-cool-gray text-sm">
        {{ a.label }}
      </span>
      <span class="block text-marine-blue my-1 text-md">
        +${{ plan.isYearlyPlan ? a.price * monthForYear : a.price }}
        {{ smallSuffix }}
      </span>
    </div>
  </div>

  <div class="flex justify-between p-6">
    <span class="block text-sm text-cool-gray">Total {{ totalSuffix }} </span>
    <span class="block text-purplish-blue text-xl font-bold">
      ${{ total }} {{ smallSuffix }}
    </span>
  </div>
</template>

<script setup>
import FormHead from "./content/FormHead.vue";
import {useCalculatePrice,useCustomSuffix} from "@/composables/usePlanPricing.vue";

const props = defineProps({
  plan: {
    type: Object,
    required: true,
  },
  addOns: {
    type: Array,
    default: () => [],
  },
});

defineEmits(["changePlan"]);

const { total, planPrice, monthForYear } = useCalculatePrice(props.plan,props.addOns);
const { totalSuffix, smallSuffix, longSuffix } = useCustomSuffix(props.plan.isYearlyPlan);
</script>
