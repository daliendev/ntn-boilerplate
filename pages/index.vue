<template>
  <main class="mt-2">
    <section class="bg-[#0a0909] xl:h-[calc(100svh-56px)] grid xl:grid-cols-2">
      <figure class="xl:p-16">
        <img src="/images/verbaland/header_picture.JPG"
        draggable="false"
        alt="Verbaland держится как царь на берузовом фоне. Красота, братцы."
        class="xl:max-h-none h-full w-svw xl:w-full object-contain" />
      </figure>
      <div v-if="lastRelease"
      class="flex items-center justify-center m-8">
      <div class="bg-secondary-200/5 text-third-100 p-3 transition-all rounded-lg">
        <nuxt-link :to="lastRelease._path" class="card card--clickable">
          <img v-if="lastRelease.cover"
          class="w-full rounded-t-md object-contain xl:max-h-[32rem] xl:object-cover" 
          draggable="false"
          :src="lastRelease.cover">
          <span class="flex-1 flex flex-col items-center py-2 xl:py-4 bg-secondary-800 text-third-100 rounded-b-md">
            <span class="bg-primary-300/90 text-secondary-950 px-3 py-[1px] rounded-md text-xs lg:text-sm">свежак!</span>
            <h3 class="text-lg xl:text-2xl">
              {{ lastRelease.title }}
            </h3>
          </span>
        </nuxt-link>
        
        <ul class="mx-8 my-4 xl:mx-16 xl:my-8 flex justify-center flex-wrap gap-2">
          <li v-for="link in lastRelease.links"
          :key="link.id">
          <a :href="link.url" class="block text-third-100 w-fit border-2 border-third-100 px-4 py-2 rounded-full hover:text-secondary-950 text-xs xl:text-base hover:bg-third-100 transition-all">
            {{ link.label }}
          </a>
        </li>
      </ul>
    </div>
  </div>
</section>
<section class="py-8 bg-secondary-950">
  <posts :amount="4" />
</section>
</main>
</template>

<script setup>
useHead({
    title: 'Verbaland'
})

const { data: lastReleases, pending, refresh, error } = await useLazyAsyncData(
  `last-release`,
  () => markRaw(
    queryContent(`releases`)
      .sort({ 'createdAt': -1 })
      .limit(1)
      .find()
      .catch((err) => console.error(err) || [])
  )
)

const lastRelease = computed(() => lastReleases.value?.length ? lastReleases.value[0] : null)
</script>