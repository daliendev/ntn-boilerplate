<template>
  <div>
    <div v-if="pending" class="cards">
      <div v-for="placeholder in placeholderClasses" :key="placeholder.id" class="card">
        <SkeletonContentPlaceholders :rounded="true" :class="placeholder">
          <SkeletonContentPlaceholdersHeading />
        </SkeletonContentPlaceholders>
      </div>
    </div>
    <ul v-else-if="posts?.length > 0" class="max-w-[900px] mx-8 lg:mx-auto grid lg:grid-cols-6 gap-8">
      <li v-for="(post, index) in posts" :key="index"  class="bg-secondary-700 text-third-100 transition-all rounded-lg lg:col-span-3">
        <nuxt-link :to="post._path" class="card card--clickable">
          <template v-if="postType === 'releases'">
            <img v-if="post.cover" class="cover-image w-full object-cover rounded-t-lg" :src="post.cover">
            <span class="flex-1">
              <h3 class="card-title text-center">{{ post.title }}</h3>
            </span>
          </template>
        </nuxt-link>
      </li>
    </ul>
    <p v-else class="max-w-5xl mx-auto">
      {{ amount > 1 ? 'Posts not found' : 'Post not found' }}
    </p>
  </div>
</template>

<script setup>
const props = defineProps({
  postType: {
    type: String,
    default: 'releases',
    validator: (val) => ['releases'].includes(val),
  },
  amount: { // ? https://content.nuxtjs.org/fetching#limitn
    type: Number,
    default: 10,
    validator: (val) => val >= 0 && val < 100,
  },
  sortBy: { // ? https://content.nuxt.com/composables/query-content#sortoptions
    type: Object,
    default: () => ({
      key: 'createdAt',
      direction: 1 // you may want `-1` here
    }),
    validator: (obj) => typeof obj.key === 'string' && typeof obj.direction === 'number',
  }
})

const { data: posts, pending, refresh, error } = await useLazyAsyncData(
  `${props.postType}-list`,
  () => markRaw(
    queryContent(`/${props.postType}`)
      .sort({ [props.sortBy.key]: props.sortBy.direction })
    .limit(props.amount)
    .find()
    .catch((err) => console.error(err) || [])
  )
)

const placeholderClasses = computed(() => {
  const classes = ['w-full','w-2/3','w-5/6'];
  return [...Array.from({ length: props.amount }, (v, i) => classes[i % classes.length])]; // repeats classes after one another
});

// const storedPosts = () => useState(`stored-${props.postType}-list`)
// const storedPosts = useState(`${props.postType}-list`);
// if (error._value) showError({ message: "Blog posts not found", cause: error });
</script>
