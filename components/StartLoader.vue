<template>
    <div class="w-full min-h-screen bg-blue-200 flex flex-col justify-center items-center">
        <Vue3Lottie :animationData="vinyl" :height="300" :width="300" />
        <h1 class="text-3xl text-blue-400 font-bold">Loading...</h1>
    </div>
</template>

<script setup>
import { Vue3Lottie } from 'vue3-lottie'
import vinyl from '../animations/vinyl.json'
</script>