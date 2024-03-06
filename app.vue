<template>
  <div>
    <h1>{{ pages.title }}</h1>
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
