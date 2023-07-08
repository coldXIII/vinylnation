<template>
    <MainLayout>
        <Intro />
        <div id="IndexPage" class="mt-4 max-w-[1200px] mx-auto px-2 ">
            <div v-if="products" class="grid xl:grid-cols-4 md:grid-cols-3  sm:grid-cols-2 grid-cols-1 gap-4 mb-6">
                <div v-for="product in products" :key="product.id">
                    <ProductComponent :product="product" />
                </div>
            </div>
            <Proposal />
            <MAJ />
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
    products.value = res.data.value
    setTimeout(() => userStore.isLoading = false, 2000)
})

</script>

<style scoped></style>