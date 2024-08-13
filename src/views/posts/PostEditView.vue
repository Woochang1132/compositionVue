<template>
  <div>
    <h2>게시글 수정</h2>
    <hr class="my-4" />
    <PostForm v-model:title="form.title" v-model:content="form.content" @submit.prevent="edit">
      <template #actions>
        <button type="button" class="btn btn-outline-danger me-2" @click="goDetailPage">
          취소
        </button>
        <button class="btn btn-primary">수정</button>
      </template>
    </PostForm>
    <AppAlert :show="showAlert" :message="alertMessage" :type="alertType"></AppAlert>
  </div>
</template>

<script setup>
import { getPostById, updatePost } from '@/api/posts'
import { ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import PostForm from '@/components/posts/PostForm.vue'
import AppAlert from '@/components/AppAlert.vue'

const route = useRoute()
const router = useRouter()
const id = route.params.id

const form = ref({
  title: null,
  content: null
})

const fetchPost = async () => {
  const { data } = await getPostById(id)
  //post.value = { ...data } // ref의 경우에는 객체 할당이 가능하다. 반응성을 잃지 않는다.
  setForm(data)
  //form = { ...data }
  //form.title = data.title
  //form.content = data.content
}
const setForm = ({ title, content }) => {
  form.value.title = title
  form.value.content = content
}
fetchPost()
const edit = async () => {
  try {
    await updatePost(id, { ...form.value })
    //router.push({ name: 'PostDetail', params: { id } })
    vAlert('수정이 완료되었습니다!!@', 'success')
  } catch (error) {
    console.error(error)
  }
}

const goDetailPage = () => router.push({ name: 'PostDetail', params: { id } })

//alert
const showAlert = ref(false)
const alertMessage = ref('')
const alertType = ref('')
const vAlert = (message, type = 'error') => {
  showAlert.value = true
  alertMessage.value = message
  alertType.value = type
  setTimeout(() => {
    showAlert.value = false
  }, 2000)
}
</script>

<style lang="scss" scoped></style>
