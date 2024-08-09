<template>
  <div class="row g-3">
    <div v-for="(item, index) in items" :key="index" class="col-4"></div>
  </div>
</template>

<script setup>
defineProps({
  items: {
    type: Array,
    required: true
  }
})
</script>
