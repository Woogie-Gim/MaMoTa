
<template>
  <div class="create-article-page">
    <h1 class="title">게시글 생성 페이지</h1>
    <form @submit.prevent="createArticle" class="article-form">
    <button @click="goBack" class="back-button">뒤로 가기</button>

      <!-- <label for="category" class="form-label">카테고리 선택:</label>
      <select name="category" id="category" v-model="category" class="form-select">
        <option
          v-for="category in categoryStore.categoryList"
          :key="category.id"
          :value="category.id"
        >
          {{ category.name }}
        </option>
      </select> -->

      <label for="title" class="form-label">글 제목:</label>
      <input type="text" name="title" v-model="title" class="form-input">
      <!-- 평점 추가코드 -->
      <label for="rate" class="form-label">평점 선택:</label>
      <select name="rate" id="rate" v-model="rate" class="form-select">
      <!-- 0.0부터 5.0까지 0.5 단위로 옵션 생성 -->
        <option v-for="i in 5" :key="i" :value="(i).toFixed(1)">
        {{ (i).toFixed(1) }}
        </option>
      </select>

      <label for="movie_title" class="form-label">영화:</label>
      <input type="text" name="movie_title" id="movie_title" class="form-input" v-model.trim="movie_title" >
      <label for="content" class="form-label">내용:</label>
      <textarea name="content" id="content" cols="30" rows="10" v-model="content" class="form-textarea"></textarea>

      <button class="submit-button">게시글 생성</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
// 카테고리 부분 데이터 어떻게 땡겨 올지 고민
// import { useCategoryStore } from '@/stores/categories'
import { useArticleStore } from '@/stores/article'
// import { onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
const router = useRouter()
const route = useRoute()
const title = ref('')
const content = ref('')
// const category = ref(1)
const rate = ref('')
const movie = ref('')
const movie_title = ref('')
const articleStore = useArticleStore()
// const categoryStore = useCategoryStore()

// onMounted(() => {
//   categoryStore.getCategoryList()
// })

// 글 생성 후 다시 커뮤니티로 
const createArticle = function () {
  const article = {
    title: title.value,
    content: content.value,
    // category: category.value
    rate: rate.value,
    movie: movie.value,
    movie_title: movie_title.value
  }
  articleStore.createArticle(article)
  router.push({name: 'community'})
}
const goBack = function () {
  router.push({name: 'community'})
}

</script>

<style scoped>

.back-button {
  background-color: #E384FF; 
  color: #865DFF;
  border-radius: 10px;
  padding: 5px;
  margin-bottom: 10px;
}

.back-button:hover {
  background-color: #865DFF; 
  color: #E384FF;
}

.create-article-page {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  color: violet;
  margin-top: 80px;
}

.title {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: white;
}

.article-form {
  background-color: rgba(79, 50, 103, 0.6);
  /* border: 1px solid #ccc; */
  border-radius: 20px;
  padding: 20px;
}

.form-label {
  font-size: 16px;
  display: block;
  margin-bottom: 8px;
}

.form-select,
.form-input,
.form-textarea {
  width: 100%;
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 10px;
  background-color: #bba6fa;
}

.submit-button {
  display: block;
  width: 100%;
  padding: 8px;
  font-size: 20px;
  font-weight: bolder;
  background-color: #E384FF;
  color: #865DFF;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.submit-button:hover {
  background-color: #865DFF;
  color: #E384FF;
}
</style>
