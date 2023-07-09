<template>
    <MainLayout>
        <Intro />
        <div class="mt-4 max-w-[1200px] mx-auto px-2 ">
            <div v-if="products" class="grid xl:grid-cols-4 md:grid-cols-3  sm:grid-cols-2 grid-cols-1 gap-4 mb-6">
                <div v-for="product in products" :key="product.id">
                    <ProductComponent :product="product" />
                </div>
            </div>
            <div v-else class="grid xl:grid-cols-4 md:grid-cols-3  sm:grid-cols-2 grid-cols-1 gap-4 mb-6">
                <Skeleton v-for="(item, index) in Array(8)" :key="index" />
            </div>
            <Proposal />
        </div>
    </MainLayout>
</template>

<script setup lang="ts">
import MainLayout from "~/layouts/MainLayout.vue"
import { IProduct } from "~/types";
import { useUserStore } from '~/stores/user';
const userStore = useUserStore()

const products = ref<IProduct[] | null>(null)

onBeforeMount(async () => {
    const res = await useFetch<IProduct[]>('/api/prisma/get-all-products')
    setTimeout(() => userStore.isLoading = false, 2000)
    products.value = res.data.value
    console.log(products.value)
})

</script>

<style scoped></style>