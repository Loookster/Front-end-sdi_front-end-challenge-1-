<script setup>
import { ref, onMounted } from 'vue';
import Pagination from './components/Pagination.vue';

const news = ref([]);
const authors = ref([]);
const totalPages = ref(57);

const fetchData = async () => {
  try {
    const [newsResponse, authorsResponse] = await Promise.all([
      fetch('https://tmsph-sdi-challenges.pages.dev/challenges/news.json'),
      fetch('https://tmsph-sdi-challenges.pages.dev/challenges/authors.json')
    ]);
    const [newsData, authorsData] = await Promise.all([
      newsResponse.json(),
      authorsResponse.json()
    ]);
    news.value = newsData;
    authors.value = authorsData;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

const getAuthorName = (authorId) => {
  const author = authors.value.find(author => author.id === authorId);
  return author ? author.name : 'Unknown';
};

onMounted(() => {
  fetchData();
});
</script>

<template>
  <div class="news-room">

      <div class="news-item" v-for="newsItem in news" :key="newsItem.id">
        <div class="image-container">
          <img :src="newsItem.image_url" v-if="newsItem.image_url" alt="News Image">
        </div>
        <div class="date-container">
          <h1>13</h1>
          <h2>JAN</h2>
        </div>
        
        <div class="share-button">Share</div>
        <div class="author">{{ getAuthorName(newsItem.author_id) }}</div>
        <h2>{{ newsItem.title }}</h2>
        <p>{{ newsItem.body }}</p>
        <a href="#">READ ARTICLE</a>
      </div>
    
  </div>
<Pagination></Pagination>

</template>
<style scoped>



.news-item {
  position: relative; 
  width: 100%;
  margin-bottom: 20px;
  padding: 20px;
}


.author {
  color: red;
}

/* Title */
h2 {
  color: #333;
  margin-top: 0;
  font-weight: bold;
}

/* Body text */
p {
  color: #555;
}


.image-container {
  position: relative;
  height: 750px;
  overflow: hidden;
}


img {
  width: auto;
  height: auto;
  max-width: 100%;
  display: block;
  margin: auto;
}

.share-button{
  display: flex;
  justify-content: right;
  font-weight: bold;
}

.date-container {
  position: absolute;
  bottom: 150px; 
  left: 50px; 
  width: 60px; 
  height: 60px;
  transform: skew(-20deg);
  background-color: red; 
  color: white;
  text-align: center;
  line-height: 60px;
}

.date-container h1,
.date-container h2 {
  position: absolute;
  color:white;
  margin: 0;
 
}

.date-container h1 {
  top: -5px;
  font-size: 25px;
  left:15px;
}

.date-container h2 {
  color:white;
  top: 15px; 
  font-size: 12px;
  left:18px;
}

@media screen and (max-width: 768px) {
  .news-item {
    padding: 15px;
  }
}


</style>