<template>
  <div>
    <div class="container mx-auto max-w-5xl">
      <div class="bg-gray mt-5">
        <div class="p-4">
          <BreadCumb :item="BreadCumbList" />
          <div class="my-4">
            <div class="flex gap-6">
              <div>
                <NuxtImg class="rounded-md" width="192" height="250" src="/images/vua-thang-cap_1571835515.jpg" />
              </div>
              <div>
                <h1 class="text-xl font-semibold pb-2">
                  Vua Thăng Cấp
                </h1>
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
                    <div class="col-span-9">15,638,939</div>
                  </li>
                </ul>
                <div class="flex gap-2 pt-1">
                  <button v-for="(item, index) in TagDetail" :key="index"
                    class="px-2 py-1 border border-orange-500 rounded text-sm hover:bg-orange-500 duration-300">
                    <NuxtLink to="/">{{ item.name }}</NuxtLink>
                  </button>
                </div>
                <div class="flex gap-2 pt-3">
                  <NuxtLink style="background-color: #8bc34a;"
                    class="px-3 py-2 min-w-[125px] flex items-center justify-center rounded-sm gap-1 hover:opacity-90"
                    to="">
                    <Icon class="text-lg" name="ic:baseline-library-books" />
                    <div>Đọc từ đầu</div>
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
            Thần đồng tên giang mới có bảy tuổi sinh trưởng quá nhanh nên bị đoản mệnh, vì là khôi phục cuộc sống bình
            thường, mang theo ký ức trong cơ thể một vị đại thần tiên xông vào Tiên giới, từ đây đi tới trở thành bá chủ
            Tiên giới mở ra con đường truyền kỳ...
          </div>
          <div class="flex gap-1 items-center py-2 mt-5">
            <Icon class="text-2xl" name="material-symbols-light:database" />
            <div class="text-lg">
              Danh sách chương
            </div>
          </div>
          <div class="border rounded">
            <div class="p-4 max-h-96 overflow-y-auto">
              <div class="py-1">
                <div class="flex justify-between border-b pb-1">
                  <NuxtLink>Chương 752</NuxtLink>
                  <div>02/11/2024</div>   
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const config = useRuntimeConfig()
const detail = ref([])
const response = await fetch(config.public.apiBase + '/get-detail-product/{slug}')
const data = await response.json()
console.log(data)
if (response.ok) {
  detail.value = data.highlightdetail
  console.log(data.highlightProducts);
} else {
  throw createError({
    statusCode: data.statusCode,
    statusMessage: data.statusMessage
  })
}
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