<template>
  <section class="bg-[#04040f] py-10">
    <div class="max-w-[900px] mx-auto grid lg:grid-cols-6 gap-8">
        <img src="/images/verbaland/contact_picture.png"
        draggable="false"
        loading="lazy"
        alt="Верба сидит на подиуме из бетонных кубов"
        class="w-2/3 mx-auto lg:w-full lg:col-span-2" />
        <div class="lg:col-span-4 h-full flex flex-col items-center justify-center">
            <p class="text-third-100 py-4 px-8 text-center">Она так долго ждала... Она ждала так, как не ждут парней из армии.. Ждала так, как Хатико не ждал своего хозяина... Долгие годы она мучилась, ожидая его... единственного и неповторимого...самого лучшего... и она дождалась.... Рэп-игра дождалась его... Вербаланда... 🦈</p>
            <a href="https://t.me/n1verba"
            aria-current="false"
            class="border-primary-300 border-[2px] text-primary-300 hover:bg-primary-300 transition-all hover:text-secondary-950 px-6 py-2 rounded-xl">Залетай в телегу</a>
        </div>
    </div>
  </section>
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
