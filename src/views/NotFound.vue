<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
    <div class="flex flex-col gap-4 w-screen h-screen justify-center items-center">
        <h1>This page doesn't exist</h1>
        <RouterLink to ="/">

            <button class="p-2 rounded-lg bg-green-600 text-white">GO BACK</button>
        </RouterLink>
    </div>
</template>