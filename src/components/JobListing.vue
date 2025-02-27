<script setup>
import { ref, computed } from 'vue'
import { RouterLink } from 'vue-router'

const props = defineProps({
  listing: Object,
  required: true
})
const showLessDescription = ref(true)
let desc = ref(props.listing.description)

const showMoreDesc = computed(() => {
  if(showLessDescription.value) {
    desc.value = props.listing.description.substring(0, 90) + '...'
  } else {
    desc.value = props.listing.description
  }
  return desc
})
const showMoreDescription = () => {
    desc.value = props.listing.description
    showLessDescription.value = !showLessDescription.value
}
</script>

<template>
            <div class="bg-white rounded-xl shadow-md relative">
            <div class="p-4">
              <div class="mb-6">
                <div class="text-gray-600 my-2">{{ listing.type }}</div>
                <h3 class="text-xl font-bold">{{ listing.title }}</h3>
              </div>

              <div class="mb-5">
                <div>{{ showMoreDesc }}</div>
                <button 
                  @click="showMoreDescription"
                  class="text-green-500"
                  >{{ showLessDescription ? 'Show more' : 'Show less'}}</button>
              </div>

              <h3 class="text-green-500 mb-2">{{ listing.salary }} / Year</h3>

              <div class="border border-gray-100 mb-5"></div>

              <div class="flex flex-col lg:flex-row justify-between mb-4">
                <div class="text-orange-700 mb-3">
                  <i class="pi pi-map-marker text-orange-700"></i>
                  {{ listing.location}}
                </div>
                <RouterLink
                  :to="`/job/${listing.id}`"
                  class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg text-center text-sm"
                >
                  Read More
                </RouterLink>
              </div>
            </div>
          </div>
</template>