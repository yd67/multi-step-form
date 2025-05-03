<script>

export const allSteps = [
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


export const allPlans = [
  {
    id: 1,
    name: "Arcade",
    price: 9,
    icon: new URL("@/assets/images/icon-arcade.svg", import.meta.url).href,
  },
  {
    id: 3,
    name: "Advanced",
    price: 12,
    icon: new URL("@/assets/images/icon-advanced.svg", import.meta.url).href,
  },
  {
    id: 4,
    name: "Pro",
    price: 15,
    icon: new URL("@/assets/images/icon-pro.svg", import.meta.url).href,
  },
];


export const allAddOns = [
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
</script>
