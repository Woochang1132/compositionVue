<template>
  <div>
    <h2>Home View</h2>
    <p>{{ $route }}</p>
    <p>{{ $route.name }}</p>
    <button class="btn btn-primary" @click="goAboutPage">about 으로 이동</button>
    <hr class="my-4" />
    <div class="row g-3">
      <div v-for="(item, index) in items" :key="index" class="col-4">
        <AppCard>{{ item }}</AppCard>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRoute, useRouter } from 'vue-router'
import { ref } from 'vue'
import AppCard from '@/components/AppCard.vue'

const route = useRoute()
const router = useRouter()
const goAboutPage = () => {
  router.push('/about')
}
const items = ref(['사과', '딸기', '포도', '바나나'])
console.log('route.path >> ', route.path)
</script>

<style lang="scss" scoped></style>
