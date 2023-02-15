<template>
  <div class="mt-32 flex flex-col items-center gap-4">
    <p>I've been clicked</p>
    <div class="text-3xl font-bold text-red">{{ count }}</div>
    <p>times.</p>
    <button class="p-4 bg-blue-500 rounded" @click="handleClick">
      Click me!
    </button>
    <div>
      Can you make the count sync across multiple tabs WITHOUT any API/server
      routes?
    </div>
  </div>
</template>

<script setup>
const count = ref(0);

onMounted(() => count.value = localStorage.getItem("myCounter"));

const handleClick = () => {
  count.value++;
  localStorage.setItem("myCounter", count.value);
};

setInterval(() => {
    count.value = localStorage.getItem("myCounter");
}, 500);
</script>

<style scoped></style>
