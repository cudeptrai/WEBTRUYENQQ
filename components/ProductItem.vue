<template>
    <div>
        <div class=" relative w-full" v-if="item">
            <NuxtLink :to="'/truyen/'+item.slug">
                <NuxtImg class="rounded-md w-full " width="168" height="218" alt="image" :src="item.url_avatar " />
            </NuxtLink>
            <div class="text-center">
                <div class="py-1 font-medium">
                    <NuxtLink :to="'/truyen/'+item.slug">{{ item.name }}</NuxtLink>
                </div>
                <div v-for="(ep, idx) in item.newEpisode" :key="idx" class="text-sm font-medium">
                    <NuxtLink :to="'/truyen/'+item.slug"> {{ ep.name }}</NuxtLink>
                </div>
            </div>
            <button class="bg-blue-400 text-xs px-2 py-1 rounded-lg absolute top-[10px] left-[10px] z-10  ">{{
                item.date }}</button>
            <button v-if="item.isHot"
                class="hot-blink bg-red text-xs px-2 py-1 rounded-lg absolute top-[10px] left-24 z-10 ">Hot</button>
        </div>
    </div>
</template>
<script setup>
defineProps({
    item: {
        type: Object,
        defaul: {}
    }
})

</script>

<style>

</style>