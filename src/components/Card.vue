<script setup>
defineProps({
  theme: String,
  default: 'bg-gray-100'
})
</script>

<template>
  <div :class="`${theme} p-6 rounded-lg shadow-md`">
    <slot></slot>
  </div>
</template>