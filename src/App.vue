<script setup>
import { ref } from 'vue'
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import HomeCards from '@/components/HomeCards.vue'
import JobListings from '@/components/JobListings.vue'

const title = ref('Become a Vue Dev')
</script>

<template>
  <Navbar />
  <Hero :title="title"/>
  <HomeCards />
  <JobListings />
</template>


