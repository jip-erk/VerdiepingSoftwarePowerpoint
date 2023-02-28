<template>
  <div class="w-full h-screen page">
    <div
      @click="emit('nextPage')"
      ref="target"
      @mouseover="setDir"
      class="absolute button"
    >
      next page
    </div>
  </div>
</template>

<script setup lang="ts">
import anime from "animejs";

const target = ref();

const pos = ref({
  x: 0,
  y: 0,
});

const { x, y } = useMouse();

onMounted(() => {
  pos.value = {
    x: window.innerWidth / 2,
    y: window.innerHeight / 2,
  };
});

const emit = defineEmits<{
  (e: "nextPage"): void;
}>();

function setDir() {
  const direction = Math.floor(Math.random() * 4);
  console.log(direction);
  const top = getRandomNumber(window.innerHeight - 100);
  const left = getRandomNumber(window.innerWidth - 100);

  animateMove(target.value, "left", left).play();
  animateMove(target.value, "top", top).play();
}

const getRandomNumber = (num: number) => {
  return Math.floor(Math.random() * (num + 1));
};

const animateMove = (element, prop, pixels) =>
  anime({
    targets: element,
    [prop]: `${pixels}px`,
    easing: "easeOutElastic(1, 0.8)",
  });

// pos.value.x =
//   mouse.x + 100 >= window.innerWidth - 100 ? mouse.x - 100 : mouse.x + 100;
// pos.value.y =
//   mouse.y + 100 >= window.innerHeight - 100 ? mouse.y - 100 : mouse.y + 100;
</script>

<style lang="scss" scoped>
.page {
  background-color: rgb(39, 39, 39);
}

.button {
  background-color: rgb(58, 58, 58);
  padding: 5px;
  border-radius: 5px;
}
</style>
