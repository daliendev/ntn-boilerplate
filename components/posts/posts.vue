<template>
  <div class="max-w-[900px] mx-8 my-8 lg:mx-auto flex flex-col items-center gap-8">
    <ul v-if="viewablePosts?.length > 0" class="grid lg:grid-cols-6 gap-8">
      <li v-for="(post, index) in viewablePosts" :key="index" class="bg-secondary-200/5   transition-all p-3 group rounded-lg lg:col-span-3">
        <nuxt-link :to="post._path">
          <img v-if="post.cover"
          class="w-full rounded-t-md object-contain" 
          draggable="false"
          :src="post.cover">
          <span class="flex-1">
            <h3 class="card-title text-center lg:text-lg py-2 bg-secondary-800 text-third-100 rounded-b-md">{{ post.title }}</h3>
          </span>
        </nuxt-link>
      </li>
    </ul>
    <p v-else class="max-w-5xl mx-auto">
      Posts not found
    </p>
    
    <button v-if="!pending && hasMorePosts" @click="loadMorePosts" class="border-primary-300 border-[2px] text-primary-300 hover:bg-primary-300 transition-all hover:text-secondary-950 px-6 py-2 rounded-xl">Показать ещё</button>
  </div>
  <ul v-if="pending" class="max-w-[900px] mx-8 lg:mx-auto grid lg:grid-cols-6 gap-8">
    <li v-for="placeholder in placeholderClasses" :key="placeholder" class="bg-secondary-500 text-third-100 transition-all rounded-lg lg:col-span-3">
      <SkeletonContentPlaceholders :centered="true" class="h-96">
        <SkeletonContentPlaceholdersHeading :img="true" />
      </SkeletonContentPlaceholders>
    </li>
  </ul>
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

const placeholderClasses = computed(() => {
  return [...Array.from({ length: props.amount })]
})

</script>
