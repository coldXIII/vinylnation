<template>
    <MainLayout>
        <div id="IndexPage" class="mt-4 max-w-[1200px] mx-auto px-2 ">
            <div class="grid xl:grid-cols-6 lg:grid-cols-5 md:grid-cols-4 sm:grid-cols-3 grid-cols-2 gap-4">
                <div v-if="products" v-for="product in products" :key="product.id">
                    <ProductComponent :product="product" />
                </div>
            </div>
        </div>
    </MainLayout>
</template>

<script setup >
import MainLayout from "~/layouts/MainLayout.vue"
import { useUserStore } from '~/stores/user';
const userStore = useUserStore()

const products = ref([])

onBeforeMount(async () => {
    const res = await useFetch('/api/prisma/get-all-products')
    setTimeout(() => products.value = res.data.value, 1000)
    setTimeout(() => userStore.isLoading = false, 1000)
    console.log(products.value)
})

</script>

<style scoped></style>