<template>
  <div>
    <h2>{{ post.title }}</h2>
    <p>{{ post.content }}</p>
    <p class="text-muted">{{ post.createdAt }}</p>
    <hr class="my-4" />
    <div class="row g-2">
      <div class="col-auto">
        <button class="btn btn-outline-dark">이전글</button>
      </div>
      <div class="col-auto">
        <button class="btn btn-outline-dark">다음글</button>
      </div>
      <div class="col-auto me-auto"></div>
      <div class="col-auto">
        <button class="btn btn-outline-dark" @click="goListPage">목록</button>
      </div>
      <div class="col-auto">
        <button class="btn btn-outline-primary" @click="goEditPage">수정</button>
      </div>
      <div class="col-auto">
        <button class="btn btn-outline-danger" @click="remove">삭제</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
import { deletePost, getPostById } from '@/api/posts'
import { ref } from 'vue'

const props = defineProps({
  id: [String, Number]
})

const router = useRouter()

/* 
ref
장) 객체 할당 가능
단) form.value.title, form.value.content

reactive
단) 객체 할당 불가능
장) form.title, form.content
*/
const post = ref({})
//let form = reactive({})
const fetchPost = async () => {
  try {
    const { data } = await getPostById(props.id)
    //post.value = { ...data } // ref의 경우에는 객체 할당이 가능하다. 반응성을 잃지 않는다.
    setPost(data)
  } catch (error) {
    console.error(error)
  }
  //form = { ...data }
  //form.title = data.title
  //form.content = data.content
}
const setPost = ({ title, content, createdAt }) => {
  post.value.title = title
  post.value.content = content
  post.value.createdAt = createdAt
}
const remove = async () => {
  try {
    if (confirm('삭제 하시겠습니까?') === false) {
      return
    }
    await deletePost(props.id)
    router.push({ name: 'PostList' })
  } catch (error) {
    console.error(error)
  }
}

fetchPost()
const goListPage = () => router.push({ name: 'PostList' })
const goEditPage = () => router.push({ name: 'PostEdit', params: { id: props.id } })
</script>

<style lang="scss" scoped></style>
