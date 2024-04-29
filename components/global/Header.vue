<template>
  <div class="bg-secondary-950 w-full z-[999999]">
    <nav>
        <ul class="grid grid-cols-3 gap-4 items-center py-4">
            <li class="col-start-2 flex justify-center">
                <a href="/" class="text-primary-300 flex items-center gap-2">
                        <icon-smiley></icon-smiley>
                        <span class="verbaland__title">verbaland</span>
                </a>
            </li>
            <!-- <li class="hidden lg:flex col-start-3 justify-end mx-8">
                <a href="/releases"
                    class="border-[2px] border-primary-300 transition-all text-primary-300 hover:text-secondary-950 hover:bg-primary-300  px-3 py-2 rounded-xl">Последние релизы</a>
            </li> -->
        </ul>
    </nav>
  </div>
</template>

<script setup>
import IconSmiley from '~/components/icons/smiley.svg'

</script>

<style scoped>

</style>
