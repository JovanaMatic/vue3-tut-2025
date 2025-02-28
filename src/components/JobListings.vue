<script setup>
import { ref, reactive, onMounted } from 'vue'
import { RouterLink } from 'vue-router'
import axios from 'axios'
import JobListing from '@/components/JobListing.vue'

defineProps({
  listing: {
    type: Number,
    default: 3
  },
  hideButton: {
    type: Boolean,
    default: false
  }
})

const state = reactive({
  jobs: [],
  isLoading: true
})
const showButton = ref(true);

const showAllJobs = () => {
  showButton.value = !showButton.value
}

onMounted(async() => {
  try {
    const response = await axios.get('http://localhost:8000/jobs')
    state.jobs = response.data
  } catch(err) {
    console.log('Error fetching jobs ', err)
  } finally {
    state.isLoading = false
  }
})
</script>

<template>
  <section class="bg-green-50 px-4 py-10">
      <div class="container-xl lg:container m-auto">
        <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
          Browse Jobs
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <JobListing
            v-for="listing in state.jobs.slice(listing ? (0, listing) : (listing))"
            :key="listing.id"
            :listing="listing"
            />
        </div>
      </div>
    </section>
    <section v-if="showButton && hideButton" class="m-auto max-w-lg my-10 px-6">
      <RouterLink
        to="/jobs"
        class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
        @click.prevent="showAllJobs"
        >View All Jobs
        </RouterLink>
    </section>
</template>