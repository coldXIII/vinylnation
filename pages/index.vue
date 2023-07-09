<template>
    <StartLoader />
</template>

<script setup>

onMounted(() => {

    setTimeout(() => {
        navigateTo('/main')
    }, 2500)
})
</script>

<style scoped></style>