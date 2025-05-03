<template>
    <div>
      <FormHead
        title="Pick add-ons"
        sub-title="Add-ons help enhance your gaming experience."
      ></FormHead>
  
      <div>
        <div
          v-for="a in addOns"
          @click="handleAddOnsSelect(a)"
          :key="a.id"
          :class="[
            'w-full flex justify-between cursor-pointer border-1 rounded-lg mb-3  p-4 hover:border-purplish-blue',
            myModel.includes(a.id) ? 'border-purplish-blue' : 'border-light-gray',
          ]"
        >
          <div class="flex items-center gap-6">
            <input
              type="checkbox"
              name="add-on-{{ a.id }}"
              :id="a.id"
              v-model="myModel"
              :checked="myModel.includes(a.id)"
              :value="a.id"
              @change.prevent
              class="w-5 h-5 border-light-gray cursor-pointer accent-purplish-blue rounded-sm"
            />
            <div>
              <label
                class="text-lg font-bold text-marine-blue"
                for="add-on-{{ a.id }}"
              >
                {{ a.label }}
              </label>
              <p class="text-sm text-cool-gray">{{ a.description }}</p>
            </div>
          </div>
          <div class="flex content-end items-center">
            <span v-if="isYearlyPlan" class="text-marine-blue"
              >+${{ a.price * 10 }}/yrs</span
            >
            <span v-else class="text-marine-blue">+${{ a.price }}/mo</span>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import FormHead from "./content/FormHead.vue";
  
  defineProps({
    addOns: Array,
    isYearlyPlan: Boolean,
  });
  
  const myModel = defineModel("selectedAddOns", {
    type: Array,
    default: () => [],
  });
  
  function handleAddOnsSelect(a) {
    const index = myModel.value.indexOf(a.id);
    if (index === -1) {
      myModel.value.push(a.id);
    } else {
      myModel.value.splice(index, 1);
    }
  }
  </script>
  