<template>
  <div class="bg-[#0a0909] w-full z-[999999] fixed">
    <nav>
      <ul class="grid grid-cols-3 gap-4 items-center py-4">
        <li class="col-start-2 flex justify-center">
          <nuxt-link to="/" class="text-primary-300 flex items-center gap-2">
            <icon-smiley></icon-smiley>
            <span class="verbaland__title">verbaland</span>
          </nuxt-link>
        </li>
      </ul>
    </nav>
  </div>
  <div class="h-12 w-full bg-[#0a0909]"></div>
</template>

<script setup>
import IconSmiley from '~/components/icons/smiley.svg'

</script>

<style scoped>

</style>
