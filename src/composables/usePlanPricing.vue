<script>
import { computed } from 'vue';

export const monthForYear = 10

export function useCalculatePrice(planData,addOnsData = []) {

    const isYearlyPlan = planData.isYearlyPlan

    const yearlyPrice = computed( () => {
        const yearsPlanPrice = planData.selectedPlan.price * monthForYear
        const yearlyAddOns = addOnsData.reduce((sum, a) => sum + (a.price * monthForYear), 0);

        return yearlyAddOns + yearsPlanPrice;
    } )

    const monthlyPrice = computed( () => {
        const monthlyAddOns = addOnsData.reduce((sum, a) => sum + (a.price), 0);
        return monthlyAddOns + planData.selectedPlan.price
    })

    const total = computed(() => {
        if (isYearlyPlan) {
            return yearlyPrice
        }
        return monthlyPrice
    })

    const planPrice = computed(() => {
        if (isYearlyPlan) {
            return (planData.selectedPlan.price * monthForYear)
        }
        return planData.selectedPlan.price
    })

    return {
        monthForYear,
        planPrice,
        total
    }
}

export function useCustomSuffix(isYearlyPlan = false) {

    const totalSuffix = computed( () => {
        if (isYearlyPlan) {
            return "(per year)"
        }
        return "(per Month)"
    })

    const smallSuffix = computed(() => {
        if (isYearlyPlan) {
            return "/yr"
        }
        return "/mo"
    })

    const longSuffix = computed(() => {
        if (isYearlyPlan) {
            return "(Yearly)"
        }
        return "(Monthly)"
    })

    return {
        totalSuffix,
        smallSuffix,
        longSuffix
    }

}

</script>