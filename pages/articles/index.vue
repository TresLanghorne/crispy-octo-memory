<template>
  <main class="min-h-screen">
    <AppHeader class="mb-16" title="Posts" :description="description" />
    <ul class="space-y-16">
      <li v-for="(article, id) in articles" :key="id">
        <AppArticleCard :article="article" />
      </li>
    </ul>
  </main>
</template>

<script setup>
const description =
   <p class="text-gray-900 dark:text-gray-400">
      By day, I'm a DevOps engineer and I love to learn and find solutions. My primary skills are C#,
      PowerShell, bicep, Azure, Git, CI/CD. I have written in a lot more but that is where my strengths
      are. I am more concerned with continually learning more than I am concerned with a specific track.
      Looking forward to more collaboration along the way.
    </p>;
useSeoMeta({
  title: "Blog | TresLanghorne",
  description,
});

const { data: articles } = await useAsyncData("all-articles", () =>
  queryContent("/articles").sort({ published: -1 }).find()
);
</script>
