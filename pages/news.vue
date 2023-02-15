<template>
  <div class="mt-32 flex flex-col items-center gap-32">
    <h1 class="text-6xl">LATEST NEWS</h1>

    <article
      v-for="post in posts"
      :key="post.id"
      class="flex flex-col gap-2 w-full max-w-[600px] border border-1 rounded-lg border-opacity-50 border-white p-8"
    >
      <h1 class="font-bold text-2xl uppercase leading-loose">
        {{ post.title }}
      </h1>
      <p class="text-lg">{{ post.body }}</p>
    </article>
    <div class="bg-red text-white p-8">
      Oh no! You've reached the end. Delete this div and load news items here!
    </div>
  </div>
</template>

<script setup>
const baseUrl = "https://dummyjson.com/posts";

const skip = ref(0);
const posts = ref([]);

const getPosts = async () => {
  const response = await $fetch(`${baseUrl}?limit=5&skip=${skip.value}`);
  posts.value = posts.value.concat(response.posts);
};

onMounted(getPosts);

const onReachEnd = ({ target }) => {
    if (target.documentElement.scrollTop + window.innerHeight >= document.body.scrollHeight - 800) {
        skip.value++;
        getPosts();
    }
};
onMounted(() => window.addEventListener('scroll', onReachEnd));
onUnmounted(() => window.removeEventListener('scroll', onReachEnd));
</script>
