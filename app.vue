// file name: app.vue
// Description: This is the main file for your Nuxt app. It fetches data from  Hygraph and displays it on the page.
<template>
  <div class="text-center">
    <h1 class="text-6xl py-12 font-bold" v-for="page in pages" :key="page.slug">
    {{ page.title }}</h1>
    <p class="text-xl" v-for="page in pages" :key="page.slug">
    {{ page.body.text }}</p>
    <button class="bg-indigo-500  hover:bg-indigo-700 text-white font-bold py-2 px-4 my-6 rounded"><a href="https://hygraph.com/docs/implementations" target="_blank">Implementation Docs</a></button>
  </div>
</template>


<script setup>
const {data} = await useFetch(
  "https://us-east-1-shared-usea1-02.cdn.hygraph.com/content/cltg6frtj07ga08upevb6yqqm/master",
  {
    method: "POST",

    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      query: `query Pages {
                pages {
                  title
                  slug
                  body {
                    text
                  }
                }
              }`,
    }),
  }
);

const pages = await data.value.data.pages;
//console.log(data.value.data.pages);
</script>
