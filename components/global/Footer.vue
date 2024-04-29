<template>
  <footer class="bg-secondary-950 text-third-100 py-10 lg:py-6 px-8">
      <div class="grid lg:grid-cols-4 max-w-[900px] mx-auto gap-8">
          <ul class="flex flex-col gap-4">
              <li class="flex items-center gap-2">
                  <icon-smiley class="text-primary-300"></icon-smiley>
                  <span class="verbaland__title">verbaland - 2024</span>
              </li>
              <li>Ощути бит!</li>
          </ul>
          <ul class="lg:col-start-3 flex flex-col gap-2 [&_li_a:hover]:underline [&_li_a:hover]:text-primary-color">
              <li class="font-bold text-lg">На всех площадках</li>
              <li><a href="https://music.apple.com/ru/artist/verbaland/1384302214">apple music</a></li>
              <li><a href="https://www.deezer.com/en/artist/14787131">deezer</a></li>
              <li><a href="https://open.spotify.com/artist/3YuxED2F6hYQXIrvdVp6Vm">spotify</a></li>
              <li><a href="https://vk.com/artist/verbaland">vk music</a></li>
              <li><a href="https://music.yandex.ru/artist/7281555">yandex music</a></li>
          </ul>
          <ul class="flex flex-col gap-2 [&_li_a:hover]:underline [&_li_a:hover]:text-primary-color">
              <li class="font-bold text-lg">Соц сети</li>
              <li><a href="https://www.instagram.com/verbaland/?hl=en">instagram</a></li>
              <li><a href="https://t.me/n1verba">telegram</a></li>
              <li><a href="https://www.tiktok.com/music/Пережитки-прошлого-6993070552395024386">tiktok</a></li>
              <li><a href="https://vk.com/verbaland">vk</a></li>
              <li><a href="https://www.youtube.com/channel/UCCNHPAFg-aQ48SdgRNEZpCQ">youtube</a></li>
          </ul>
      </div>
  </footer>
</template>

<script setup>
import IconSmiley from '~/components/icons/smiley.svg'
</script>

<style scoped>

</style>
