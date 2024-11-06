<script setup>
// import jobData from './../../public/jobs.json'
import { ref, computed, onMounted, reactive } from 'vue';
import JobListing from './JobListing.vue';
import { defineProps} from 'vue';
import { RouterLink } from 'vue-router';
import axios from 'axios';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import API_BASE_URL from './../api'

defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false
    }
});


const state = reactive({
    jobs: [],
    isLoading: true
})


console.log('Using API base URL:', API_BASE_URL);

onMounted(async () => {
    try {
        const response = await axios.get(`${API_BASE_URL}/jobs`)

            state.jobs = response.data;
            console.log(jobs.value);
    
    } catch (error) {
        console.error('error fetching data: ' + error)
        
    } finally {
        state.isLoading = false;
    }
})

</script>

<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div v-if="state.isLoading" class="text-center text-gray py-6">
                <PulseLoader/> 
                <p class="font-semibold">This may take up to 90 seconds if the server was asleep..</p>
            </div>
            <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job"/>
            </div>

        </div>

    </section>

    <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
        <RouterLink
            to="/jobs"
            class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
            >View All Jobs
        </RouterLink>
    </section>
  
  
</template>