<template>
  <div>
    <h2>Home View</h2>
    <p>{{ $route }}</p>
    <p>{{ $route.name }}</p>
    <button class="btn btn-primary" @click="goAboutPage">about 으로 이동</button>
    <hr class="my-4" />
    <AppGrid :items="items" v-slot="{ item }" col-class="col-3">
      <AppCard>{{ item }}</AppCard>
    </AppGrid>
  </div>
</template>

<script setup>
import { useRoute, useRouter } from 'vue-router'
import { ref } from 'vue'
import AppCard from '@/components/AppCard.vue'
import AppGrid from '@/components/AppGrid.vue'

const route = useRoute()
const router = useRouter()
const goAboutPage = () => {
  router.push('/about')
}
const items = ref(['사과', '딸기', '포도', '바나나'])
console.log('route.path >> ', route.path)
</script>

<style lang="scss" scoped></style>
