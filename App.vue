<template>
  <div class="fixed bottom-0 right-0 p-5">
    {{ currentPage + 1 }} / {{ pages.length }}
  </div>
  <NuxtLayout>
    <NuxtPage @click="click" @nextPage="click(false)" />
  </NuxtLayout>
</template>

<script lang="ts" setup>
const pages = [
  { name: "index", route: "/" },
  { name: "jip", route: "/jip" },
  { name: "test", route: "/test" },
];
const router = useRouter();

const currentPage = computed(() => {
  return pages
    .map((e) => e.route)
    .indexOf(String(router.currentRoute.value.path));
});

function click(isButton?: boolean) {
  if (pages[currentPage.value].name === "jip" && isButton) return;
  if (currentPage.value + 1 >= pages.length) return;
  router.push({ path: pages[currentPage.value + 1].route });
}
</script>

<style>
body {
  overflow: hidden;
}

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
