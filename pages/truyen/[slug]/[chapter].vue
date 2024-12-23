<template>
  <div>
    <div v-if="isLoading">
      <Loading />
    </div>
    <div v-else class="container mx-auto max-w-5xl">
      <div class="bg-gray mt-5">
        <div class="p-4">
          <BreadCumb :item="BreadCumbList" />
          <div class="my-2 font-semibold">
            {{ detail.name }} <span class="text-sm font-light">(Cập nhật lúc: {{ detail.update_time }})</span>
          </div>
          <div class="bg-zinc-600 gap-1 py-2 rounded my-2 flex items-center justify-center">
            <Icon name="bi:info-circle-fill" /> Sử dụng mũi tên trái (←) hoặc phải (→) để chuyển chapter
          </div>
          <div class="flex items-center justify-center gap-2 mt-3">
            <NuxtLink v-if="prev_slug" :to="'/truyen/' + route.params.slug + '/' + prev_slug"
              class="px-2 py-1 rounded text-gray flex items-center justify-center gap-1 font-medium bg-primary">
              <Icon name="fa6-solid:arrow-left" /> Chap trước
            </NuxtLink>
            <span v-else
              class="px-2 py-1 rounded text-gray flex items-center justify-center gap-1 font-medium bg-zinc-300 cursor-not-allowed">
              <Icon name="fa6-solid:arrow-left" /> Chap trước
            </span>
            <NuxtLink v-if="next_slug" :to="'/truyen/' + route.params.slug + '/' + next_slug"
              class="px-2 py-1 rounded text-gray flex items-center justify-center gap-1 font-medium bg-primary">
              Chap sau
              <Icon name="fa6-solid:arrow-right" />
            </NuxtLink>
            <span v-else
              class="px-2 py-1 rounded text-gray flex items-center justify-center gap-1 font-medium bg-zinc-300 cursor-not-allowed">
              Chap sau
              <Icon name="fa6-solid:arrow-right" />
            </span>
          </div>
        </div>
      </div>
      <div class="grid justify-center items-center my-4">
        <div v-for="(item, index) in images" :key="index">
          <NuxtImg :src="item" />
        </div>
      </div>
      <div class="bg-gray mt-5">
        <div class="p-4">
          <div class="flex items-center justify-center gap-2 mt-3">
            <NuxtLink v-if="prev_slug" :to="'/truyen/' + route.params.slug + '/' + prev_slug"
              class="px-2 py-1 rounded text-gray flex items-center justify-center gap-1 font-medium bg-primary">
              <Icon name="fa6-solid:arrow-left" /> Chap trước
            </NuxtLink>
            <span v-else
              class="px-2 py-1 rounded text-gray flex items-center justify-center gap-1 font-medium bg-zinc-300 cursor-not-allowed">
              <Icon name="fa6-solid:arrow-left" /> Chap trước
            </span>
            <NuxtLink v-if="next_slug" :to="'/truyen/' + route.params.slug + '/' + next_slug"
              class="px-2 py-1 rounded text-gray flex items-center justify-center gap-1 font-medium bg-primary">
              Chap sau
              <Icon name="fa6-solid:arrow-right" />
            </NuxtLink>
            <span v-else
              class="px-2 py-1 rounded text-gray flex items-center justify-center gap-1 font-medium bg-zinc-300 cursor-not-allowed">
              Chap sau
              <Icon name="fa6-solid:arrow-right" />
            </span>
          </div>
          <BreadCumb :item="BreadCumbList" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>

const config = useRuntimeConfig()
const route = useRoute()
const detail = ref([])
const prev_slug = ref('')
const next_slug = ref('')
const isLoading = ref(true)
const images = ref([])
const loadData = async () => {
  try {
    const response = await fetch(config.public.apiBase + '/get-episode/' + route.params.slug + '/' + route.params.chapter)
    const data = await response.json()
    detail.value = data.episode
    if (data.prev_episode) {
      prev_slug.value = data.prev_episode.slug
    }
    if (data.next_episode) {
      next_slug.value = data.next_episode.slug
    }
    images.value = data.episode.servers[0].images
    useSeoMeta({
      title: data.title,
      ogTitle: data.meta_title,
      description: data.desc,
      ogDescription: data.meta_desc,
      ogImage: data.meta_image,
    })
    isLoading.value = false
  } catch (error) {
    console.log(error)
    // throw createError(error)
  }
}
onMounted(async () => {
  await loadData()
})
const BreadCumbList = [
  {
    name: 'Ta Là Tà Đế',
    link: '/detail'
  },
  {
    name: 'Chương 176',
    link: '/detail'
  },
]
</script>

<style></style>