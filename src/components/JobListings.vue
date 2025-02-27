<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import jobData from '@/jobs.json'
import JobListing from '@/components/JobListing.vue'

const jobs = ref(jobData.slice(0,3));
const showButton = ref(true);

const showAllJobs = () => {
  jobs.value = jobData
  showButton.value = !showButton.value
}
</script>

<template>
  <section class="bg-green-50 px-4 py-10">
      <div class="container-xl lg:container m-auto">
        <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
          Browse Jobs
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <JobListing
            v-for="listing in jobs"
            :key="listing.id"
            :listing="listing"
            />
        </div>
      </div>
    </section>
    <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
      <RouterLink
        to="/jobs"
        class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
        @click.prevent="showAllJobs"
        >View All Jobs
        </RouterLink>
    </section>
</template>