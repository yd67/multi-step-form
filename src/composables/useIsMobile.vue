<script>
import { ref, computed, onMounted, onUnmounted } from "vue";

export function useIsMobile() {
  const screenWidth = ref(window.innerWidth);

  const change = () => {
    screenWidth.value = window.innerWidth;
  };

  onMounted(() => {
    window.addEventListener("resize", change);
  });
  
  onUnmounted(() => {
    window.removeEventListener("resize", change);
  });

  const isMobile = computed(() => screenWidth.value < 767);

  return { isMobile };
}
</script>