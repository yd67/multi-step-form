<script>
import { computed } from "vue";

export const monthForYear = 10;


export function useCalculatePrice(planData, addOnsData = []) {
  const isYearlyPlan = planData.isYearlyPlan;

  const yearlyPrice = computed(() => {
    const yearsPlanPrice = planData.selectedPlan.price * monthForYear;

    const yearlyAddOns = addOnsData.reduce(
      (sum, a) => sum + a.price * monthForYear,
      0
    );

    return yearlyAddOns + yearsPlanPrice;
  });

  const monthlyPrice = computed(() => {
    const monthlyAddOns = addOnsData.reduce((sum, a) => sum + a.price, 0);
    return monthlyAddOns + planData.selectedPlan.price;
  });

  const total = computed(() => (isYearlyPlan ? yearlyPrice : monthlyPrice));

  const planPrice = computed(() =>
    isYearlyPlan
      ? planData.selectedPlan.price * monthForYear
      : planData.selectedPlan.price
  );

  return {
    monthForYear,
    planPrice,
    total,
  };
}


export function useCustomSuffix(isYearlyPlan = false) {
  const totalSuffix = computed(() =>
    isYearlyPlan ? "(per year)" : "(per Month)"
  );
  const smallSuffix = computed(() => (isYearlyPlan ? "/yr" : "/mo"));
  const longSuffix = computed(() => (isYearlyPlan ? "(Yearly)" : "(Monthly)"));

  return {
    totalSuffix,
    smallSuffix,
    longSuffix,
  };
}
</script>
