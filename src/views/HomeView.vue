<script setup>
import Hero from '@/components/Hero.vue'
import HomeCards from '@/components/HomeCards.vue'
import JobListings from '@/components/JobListings.vue'
import { ref } from 'vue'

const title = ref('Become Vue Developer')
</script>

<template>
  <Hero :title="title"/>
  <HomeCards />
  <JobListings listing="3" :hideButton="true" />
</template>