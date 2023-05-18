<script setup lang="ts">
import {RouterView} from 'vue-router'
import Header from "@/views/layouts/Header.vue";
import Footer from "@/views/layouts/Footer.vue";
</script>

<template>
    <Header></Header>
    <RouterView/>
    <Footer></Footer>
</template>

<style scoped>
</style>
