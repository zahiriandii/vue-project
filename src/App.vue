
<script setup>
    import navBar from '@/components/navBar.vue';
    import './assets/main.css';
    import HeroPart from './components/heroPart.vue';
    import HomeCards from './components/HomeCards.vue';
    import JobListings from './components/JobListings.vue';
</script>

<template>
    <navBar />
    <HeroPart />
    <HomeCards />
    <JobListings :limit="3"  showJobs="true"/>
</template>