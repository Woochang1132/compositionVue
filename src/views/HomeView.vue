<template>
  <div>
    <h2>Home View</h2>
    <p>{{ $route }}</p>
    <p>{{ $route.name }}</p>
    <button class="btn btn-primary" @click="goAboutPage">about 으로 이동</button>
  </div>
</template>

<script setup>
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()
const goAboutPage = () => {
  router.push('/about')
}
console.log('route.path >> ', route.path)
</script>

<style lang="scss" scoped></style>
