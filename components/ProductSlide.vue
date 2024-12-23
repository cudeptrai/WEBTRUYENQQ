<template>
    <div>
        <swiper :style="{ '--swiper-navigation-color': '#2c2c2c' }" :breakpoints="{
            0: {
                slidesPerView: 2, 
                spaceBetween: 10
            },
            1024: {
                slidesPerView: 5,
                spaceBetween: 20
            }
        }" :autoplay="{
            delay: 2000,
            disableOnInteraction: true,
        }" :navigation="true" :modules="[SwiperAutoplay, SwiperNavigation]" class="mySwiper">
            <SwiperSlide v-for="(item, index) in data" :key="index">
                <NuxtLink :to="'/truyen/' + item.slug">
                    <NuxtImg class="rounded-md w-full " width="168" height="218" alt="image" :src="item.url_avatar" />
                </NuxtLink>
                <div class="text-center">
                    <div class="py-1 font-medium">
                        <NuxtLink :to="'/truyen/' + item.slug">{{ item.name }}</NuxtLink>
                    </div>
                    <div v-for="(ep, idx) in item.newEpisode" :key="idx" class="text-sm font-medium">
                        <NuxtLink :to="'/truyen/' + item.slug"> {{ ep.name }}</NuxtLink>
                    </div>
                </div>
                <button
                    class="bg-blue-400 text-xs lg:px-1 px-3 lg:py-1 py-2 rounded-xl absolute top-[10px] left-[10px] z-10">{{
                        item.time_difference }}</button>
                <button
                    class="hot-blink bg-red text-xs px-2 lg:py-1 py-2  rounded-xl absolute top-[10px] right-1 z-10 ">Hot</button>
            </SwiperSlide>
        </swiper>
    </div>
</template>

<script lang="ts" setup>

defineProps({
    data: {
        type: Object,
        default: {}
    },
})
</script>

<style></style>