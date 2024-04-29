<template>
  <main>
    <section class="py-8 bg-secondary-950">
      <posts post-type="releases" :amount="10" />
    </section>

    <section class="bg-[#000] py-10">
    <div class="max-w-[900px] mx-auto grid lg:grid-cols-6 gap-8">
        <img src="/images/verbaland/contact_picture.png" loading="lazy" class="w-2/3 mx-auto lg:w-full lg:col-span-2" />
        <div class="lg:col-span-4 h-full flex flex-col items-center justify-center">
            <p class="text-third-100 py-4 px-8 text-center">Она так долго ждала... Она ждала так, как не ждут парней из армии.. Ждала так, как Хатико не ждал своего хозяина... Долгие годы она мучилась, ожидая его... единственного и неповторимого...самого лучшего... и она дождалась.... Рэп-игра дождалась его... Вербаланда... 🦈</p>
            <a href="https://t.me/n1verba"
            class="border-primary-300 border-[2px] text-primary-300 hover:bg-primary-300 transition-all hover:text-secondary-950 px-6 py-2 rounded-xl">Залетай в телегу</a>
        </div>
    </div>
</section>
  </main>
</template>