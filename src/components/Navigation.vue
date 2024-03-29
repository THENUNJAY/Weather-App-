<template>
    <div class="sticky top-0 bg-weather-primary shadow-lg">
        <nav
        class="container flex flex-col sm:flex-row items-center 
          gap-4 text-white py-6"
        
        >
        <router-link :to="{name:'home'}">
            <div class="flex items-center gap-3 flex-1">
            <p class="text-2xl">Weather Guide</p>
            <span class="fa-solid fa-sun text-2xl"></span>
            </div>
        </router-link>
        
        </nav>
    </div>
</template>

<script setup>
import {RouterLink } from "vue-router";

// const places = ref([])
const addPlace = (data) => {
    places.value.push(data)
}
</script>

