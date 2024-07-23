<template>
  <div class="bg-[#04040f] w-full">
    <nav>
      <ul class="grid xl:grid-cols-3 gap-4 items-center py-4">
        <li class="px-16 flex justify-center xl:justify-start">
          <nuxt-link to="/" class="text-primary-300 text-xl xl:text-3xl flex items-center gap-2">
            <icon-smiley></icon-smiley>
            <span class="verbaland__title">verbaland</span>
          </nuxt-link>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script setup>
import IconSmiley from '~/components/icons/smiley.svg'

</script>

<style scoped>

</style>
