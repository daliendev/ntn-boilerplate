<template>
  <main class="mt-2">
    <section class="bg-[#0a0909] grid lg:grid-cols-2">
      <img src="/images/verbaland/header_picture.JPG"
      draggable="false"
      alt="Verbaland держится как царь на берузовом фоне. Красота братцы."
      class="xl:max-h-none xl:h-[calc(100svh-56px)] w-svw xl:w-full object-cover" />
      <div v-if="lastRelease"
      class="flex items-center justify-center m-8">
      <div class="bg-secondary-800 text-third-100 transition-all rounded-lg">
        <nuxt-link :to="lastRelease._path" class="card card--clickable">
          <img v-if="lastRelease.cover"
          class="cover-image w-full h-72 xl:h-[32rem] object-cover rounded-t-lg" 
          draggable="false"
          :src="lastRelease.cover">
          <span class="flex-1 flex flex-col items-center py-2 xl:py-4">
            <span class="text-primary-300/90 text-xs lg:text-sm">свежак!</span>
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
import { computed } from 'vue'

const { data: lastReleases, pending, refresh, error } = await useLazyAsyncData(
  `last-release`,
  () => markRaw(
    queryContent(`/releases`)
      .limit(1)
      .find()
      .catch((err) => console.error(err) || [])
  )
)

const lastRelease = computed(() => lastReleases.value?.length ? lastReleases.value[0] : null)
</script>