<script setup>
    import jobListings from '@/jobs.json';
    import Job from './Job.vue';
    import { ref, defineProps } from 'vue';

    const jobData = ref(jobListings);

    defineProps({
        limit : Number ,
        showJobs : {
            type: Boolean,
            default: false
        }
    });
    
</script>

<template>

    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 md-6 text-center">

            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <Job v-for="job in jobData.slice(0,limit || jobData.length)" :key="job.id" :job="job"/>
            </div>
        </div>
    </section>
    <section v-if="showJobs" class="m-auto max-w-lg my-10 px-6">
      <a
        :href="'/jobs'"
        class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
        >View All Jobs</a
      >
    </section>
    
</template>