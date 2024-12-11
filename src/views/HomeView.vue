
<script setup>
    import heroPart from '@/components/heroPart.vue';
    import HomeCards from '@/components/HomeCards.vue';
    import JobListings from '@/components/JobListings.vue';
</script>

<template>

    <HeroPart />
    <HomeCards />
    <JobListings :limit="3"  showJobs="true"/>
</template>