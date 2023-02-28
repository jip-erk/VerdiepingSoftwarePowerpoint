<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>

<script lang="ts" setup>
const pressed = reactive(useMousePressed());
const pages = [
  { name: "index", route: "/" },
  { name: "test", route: "/test" },
];
const currentPage = ref(1);
const router = useRouter();
watch(pressed, () => {
  router.push({ path: pages[currentPage.value].route });
});
</script>

<style>
.page-left-enter-active,
.page-right-enter-active,
.page-left-leave-active,
.page-right-leave-active {
  transition: all 0.3s linear;
}

.page-left-enter-from,
.page-right-leave-to {
  transform: translateX(100%);
}

.page-left-leave-to,
.page-right-enter-from {
  transform: translateX(-100%);
}

.page-left-enter-to,
.page-right-enter-to {
  transform: translateX(0);
}
</style>
