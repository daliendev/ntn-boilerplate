<template>
  <section v-if="post" class="max-w-[900px] my-8 mx-auto">
    <article class="flex flex-col">
      <figure class="mx-8 lg:mx-0 flex items-center">
        <img v-if="post.cover"
        class="w-full max-h-[600px] object-contain"
        draggable="false"
        :src="post.cover" />
      </figure>
      
      <h1 class="mx-8 text-center text-2xl lg:text-5xl text-primary-300 font-bold my-4">{{ post.title }}</h1>
      <ContentRenderer :value="post">
        <ContentRendererMarkdown :value="post" />
        <template #empty>
        </template>
      </ContentRenderer>
      
      <ul class="mx-8 xl:mx-16 my-8 flex justify-center flex-wrap gap-2">
        <li v-for="link in post.links"
        :key="link.id">
          <a :href="link.url" class="block text-third-100 w-fit border-2 border-third-100 px-4 py-2 rounded-full hover:text-secondary-950 hover:bg-third-100 transition-all text-sm xl:text-base">
            {{ link.label }}
          </a>
        </li>
      </ul>
    </article>
  </section>
</template>

<script setup>
const route = useRoute()

const { data: post, pending, refresh, error } = await useAsyncData(
  'post',
  () => queryContent('/releases', route.params.release)
    .findOne()
    .catch((err) => console.error(err) || [])
)

watchEffect(() => {
  refresh()
})
</script>
