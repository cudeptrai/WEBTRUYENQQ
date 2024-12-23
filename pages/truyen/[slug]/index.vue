<template>
  <div>
    <div v-if="isLoading">
      <Loading />
    </div>
    <div v-else class="container mx-auto max-w-5xl">
      <div class="bg-gray mt-5">
        <div class="p-4">
          <BreadCumb :item="BreadCumbList" />
          <div class="my-4">
            <div class="flex gap-6">
              <div>
                <NuxtImg class="rounded-md" width="192" height="250" :src="details.url_avatar" />
              </div>
              <div>
                <h1 class="text-xl font-semibold pb-2">
                  {{ details.full_name }} </h1>
                <ul>
                  <li class="grid grid-cols-12 py-1 items-center justify-between gap-16">
                    <div class="col-span-3">
                      <div class="flex gap-1 items-center">
                        <Icon class="text-xl" name="material-symbols:person" />
                        <div>Tác Giả</div>
                      </div>
                    </div>
                    <div class="col-span-9">Đang cập nhật</div>
                  </li>
                  <li class="grid grid-cols-12 py-1 items-center justify-between gap-16">
                    <div class="col-span-3">
                      <div class="flex gap-1 items-center">
                        <Icon class="text-xl" name="line-md:uploading" />
                        <div>Tình trạng</div>
                      </div>
                    </div>
                    <div class="col-span-9">Đang cập nhật</div>
                  </li>
                  <li class="grid grid-cols-12 py-1 items-center justify-between gap-16">
                    <div class="col-span-3">
                      <div class="flex gap-1 items-center">
                        <Icon class="text-xl" name="ion:md-thumbs-up" />
                        <div>Lượt thích</div>
                      </div>
                    </div>
                    <div class="col-span-9">13668</div>
                  </li>
                  <li class="grid grid-cols-12 py-1 items-center justify-between gap-16">
                    <div class="col-span-3">
                      <div class="flex gap-1 items-center">
                        <Icon class="text-xl" name="mdi:cards-heart" />
                        <div>Lượt theo dõi</div>
                      </div>
                    </div>
                    <div class="col-span-9">61,987</div>
                  </li>
                  <li class="grid grid-cols-12 py-1 items-center justify-between gap-16">
                    <div class="col-span-3">
                      <div class="flex gap-1 items-center">
                        <Icon class="text-xl" name="mdi:eye-outline" />
                        <div>Lượt xem</div>
                      </div>
                    </div>
                    <div class="col-span-9">{{ details.views }}</div>
                  </li>
                </ul>
                <div class="flex gap-2 pt-1" v-if="details.types.length > 0">
                  <button v-for="(item, index) in details.types" :key="index"
                    class="px-2 py-1 border border-orange-500 rounded text-sm hover:bg-orange-500 duration-300">
                    <NuxtLink to="/">{{ item.types }}</NuxtLink>
                  </button>
                </div>
                <div class="flex gap-2 pt-3">
                  <NuxtLink style="background-color: #8bc34a;"
                    class="px-3 py-2 min-w-[125px] flex items-center justify-center rounded-sm gap-1 hover:opacity-90"
                    to="">
                    <Icon class="text-lg" name="ic:baseline-library-books" />
                    <div><NuxtLink :to="'/truyen/'+details.slug+'/'+ details.episodes[details.episodes.length-1].slug">Đọc từ đầu</NuxtLink> </div>
                  </NuxtLink>
                  <NuxtLink style="background-color: #ff3860;"
                    class="px-3 py-2 min-w-[125px] flex items-center justify-center rounded-sm gap-1 hover:opacity-90"
                    to="">
                    <Icon class="text-lg" name="material-symbols:favorite" />
                    <div>Theo dõi</div>
                  </NuxtLink>
                  <NuxtLink style="background-color: #bd10e0;"
                    class="px-3 py-2 min-w-[125px] flex items-center justify-center rounded-sm gap-1 hover:opacity-90"
                    to="">
                    <Icon class="text-lg" name="flowbite:thumbs-up-solid" />
                    <div>Thích</div>
                  </NuxtLink>
                  <NuxtLink style="background-color: #209cee;"
                    class="px-3 py-2 min-w-[125px] flex items-center justify-center rounded-sm gap-1 hover:opacity-90"
                    to="">
                    <Icon class="text-lg" name="mingcute:send-plane-fill" />
                    <div>Đọc tiếp</div>
                  </NuxtLink>
                </div>
              </div>
            </div>
          </div>
          <div class="flex gap-1 items-center py-2">
            <Icon class="text-xl" name="f7:info-circle-fill" />
            <div class="text-lg">
              Giới Thiệu
            </div>
          </div>
          <div class="flex gap-1 items-center">
            {{ details.meta_desc }}
          </div>
          <div class="flex gap-1 items-center py-2 mt-5">
            <Icon class="text-2xl" name="material-symbols-light:database" />
            <div class="text-lg">
              Danh sách chương
            </div>
          </div>
          <div class="border rounded">
            <div class="p-4 max-h-96 overflow-y-auto">
              <div v-for="(item, index) in details.episodes" :key="index" class="py-1">
                <div class="flex justify-between border-b pb-1">
                  <NuxtLink :to="'/truyen/'+details.slug+'/'+ details.episodes[0].slug">{{ item.name }}</NuxtLink>
                  <div>{{ item.update_time }}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const config = useRuntimeConfig()
const isLoading = ref(true)
const details = ref([])
const route = useRoute()
const loadData = async () => {
  try {
    const response = await fetch(config.public.apiBase + '/get-detail-product/' + route.params.slug)
    const data = await response.json()
    details.value = data.product
    useSeoMeta({
      title:data.title,
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
onMounted(async() => {
 await loadData()
})

const TagDetail = [
  { name: 'Action' },
  { name: 'Adventure' },
  { name: 'Fantasy' },
  { name: 'Manhwa' },
  { name: 'Webtoon' },
]
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