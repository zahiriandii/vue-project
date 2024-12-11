
<script setup>
    import navBar from '@/components/navBar.vue';
    import './assets/main.css';
    import { RouterView } from 'vue-router';
</script>

<template>
    <navBar />
    <RouterView />
</template>