<template>
  <div class="max-w-[900px] mx-8 my-8 lg:mx-auto flex flex-col items-center gap-8">
    <ul v-if="viewablePosts?.length > 0" class="grid lg:grid-cols-6 gap-8">
      <li v-for="(post, index) in viewablePosts" :key="index" class="bg-secondary-200/5 hover:bg-primary-50/10 transition-all p-3 group rounded-lg lg:col-span-3">
        <nuxt-link :to="post._path">
          <img v-if="post.cover"
          class="w-full rounded-md object-contain" 
          draggable="false"
          :src="post.cover">
          <span class="flex-1">
            <h3 class="card-title text-center mt-2 lg:text-lg py-2 bg-secondary-800 text-third-100 rounded-md">{{ post.title }}</h3>
          </span>
        </nuxt-link>
      </li>
    </ul>
    <p v-else class="max-w-5xl mx-auto">
      Posts not found
    </p>
    
    <button v-if="pending || hasMorePosts"
      @click="loadMorePosts"
      :disabled="pending"
      class="border-primary-300 border-[2px] text-primary-300 hover:bg-primary-300 transition-all hover:text-secondary-950 py-2 rounded-xl flex gap-4 pl-10 pr-6">
      Показать ещё
      <svg v-if="pending" class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
      </svg>
      <span v-else></span>
    </button>
  </div>
</template>

<script setup>

const props = defineProps({
  amount: { // ? https://content.nuxtjs.org/fetching#limitn
    type: Number,
    default: 10,
    validator: (val) => val >= 0 && val < 100,
  },
  sortBy: { // ? https://content.nuxt.com/composables/query-content#sortoptions
    type: Object,
    default: () => ({
      key: 'createdAt',
      direction: -1 
    }),
    validator: (obj) => typeof obj.key === 'string' && typeof obj.direction === 'number',
  }
})

const pageAmount = ref(1)

const { data: viewablePosts, pending, refresh, error } = await useLazyAsyncData(
  `releases-list`,
  () => markRaw(
    queryContent(`releases`)
      .sort({ [props.sortBy.key]: props.sortBy.direction })
      .skip(1)
      .limit(4)
      .find()
      .catch((err) => console.error(err) || [])
  )
)


const { data: totalPosts } = await useLazyAsyncData(
`releases-list-count`,
async () => {
  try {
    const count = await queryContent(`releases`)
    .only('title')
    .skip(1)
    .count()
    return count
  } catch (err) {
    console.error(err)
    return 0
  }
}
)

const loadMorePosts = async () => {
  pending.value = true 
  if(pageAmount.value === 1) pageAmount.value = props.amount + 1
  else pageAmount.value += props.amount
  console.log(pageAmount.value)
  
  const fetchedPosts = await queryContent(`releases`)
    .sort({ [props.sortBy.key]: props.sortBy.direction })
    .skip(pageAmount.value)
    .limit(props.amount)
    .find()
    .catch((err) => console.error(err) || [])
  
  viewablePosts.value.push(...fetchedPosts)
  pending.value = false
}

const hasMorePosts = computed(() => totalPosts.value > viewablePosts.value?.length + 1)

</script>
