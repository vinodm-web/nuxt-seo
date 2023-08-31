<template>
  <Body
    class="antialiased duration-300 transition-colors text-gray-800 dark:text-gray-200 bg-white dark:bg-gray-950"
  >
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </Body>
</template>

<script setup lang="ts">
  // useHead({
  //   title: 'My App',
  //   meta: [
  //     { name: 'description', content: 'My amazing site.' }
  //   ],
  //   bodyAttrs: {
  //     class: 'test'
  //   },
  //   script: [ { type: 'module', innerHTML: 'console.log(\'Hello world\')' } ]
  // })

  const route = useRoute()
  const itemId = route.params.id | 1

  const productDetails = await fetch(`https://dummyjson.com/products/${itemId}`)
                                .then(res => res.json())
                                .then(data => data)
  const title = `${productDetails.title} | ${productDetails.description}`

  useServerSeoMeta({
    ogTitle: () => title,
    title: () => title,
    description: () => productDetails.description,
    ogDescription: () => productDetails.description,
    ogImage: () => productDetails.thumbnail,
    ogImageUrl: () => productDetails.thumbnail,
    twitterCard: () => 'summary_large_image',
    twitterTitle: () => title,
    twitterDescription: () => productDetails.description,
    twitterImage: () => productDetails.thumbnail,
  })
</script>
