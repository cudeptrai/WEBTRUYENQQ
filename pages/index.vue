<template>
  <div class="container mx-auto max-w-5xl">
    <div class="mt-5">
      <div class="flex items-center gap-1">
        <Icon class="text-3xl text-red" name="ic:round-star" />
        <div class="text-2xl text-red font-bold">Truyện Hay</div>
      </div>
      <div class="mt-3 ">
        <ProductSlide :data="highlightProducts" />
      </div>
      <div class="flex items-center gap-1 my-5">
        <Icon class="text-3xl" name="ic:baseline-cloud-download" />
        <div class="text-2xl font-bold">Truyện mới cập nhật </div>
      </div>
      <div class="mt-3">
        <div class="grid grid-cols-2 lg:grid-cols-5 gap-4">
          <div v-for="(item, index) in newProducts" :key="index">
            <ProductItem :item="item" />
          </div>
        </div>
      </div>
    </div>
    <div class="text-center my-10">
      <NuxtLink class="p-3 bg-primary rounded-md font-semibold my-6 hover:bg-orange-600" to="/">Xem thêm nhiều truyện
      </NuxtLink>
    </div>
  </div>
</template>
<script lang="ts" setup>
useSeoMeta({
  title: 'My Amazing Site',
  ogTitle: 'My Amazing Site',
  description: 'This is my amazing site, let me tell you all about it.',
  ogDescription: 'This is my amazing site, let me tell you all about it.',
  ogImage: 'https://example.com/image.png',
  twitterCard: 'summary_large_image',
})
const config = useRuntimeConfig()
const highlightProducts = ref([])
const newProducts = ref([])
const loadData = async () => {
  try {
    const response = await fetch(config.public.apiBase + '/get-data-home')
    const data = await response.json()
    highlightProducts.value = data.highlightProducts
    newProducts.value = data.newProducts
    console.log(data.highlightProducts);
  } catch (error) {
    console.log(error)
    // throw createError(error)
  }
}
onMounted(() => {
  loadData()
})




</script>

<style>
.swiper-button-next,
.swiper-button-prev {
  background-color: #ffffffa6;
  /* Màu nền nút navigation */
  padding: 20px;
}

.swiper-button-prev:after,
.swiper-button-next:after {
  font-size: 22px;

}

.swiper-button-next:hover,
.swiper-button-prev:hover {
  background-color: #e2dbdb;
  color: black;
}
</style>