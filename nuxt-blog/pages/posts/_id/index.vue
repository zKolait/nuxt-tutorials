<template>
  <div class="single-post-page">
    <section class="post">
      <img :src="loadedPost.thumbnail">
      <h2 class="post-title">{{ loadedPost.title }}</h2>
      <div class="post-details">
        <div class="post-detail">Last updated on : {{ loadedPost.updateDate | date }}</div>
        <div class="post-detail">Written by : {{ loadedPost.author }} </div>
      </div>
      <p>{{ loadedPost.content }}</p>
    </section>
    <section class="post-feedback">
      <p>Send me your review about the post. <a href="mailto:mail@gmail.com">Mail</a></p>
    </section>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  asyncData(context) {
    return axios
      .get(process.env.baseUrl + 'posts/' + context.params.id + '.json')
      .then(res => {
        return {
          loadedPost: res.data
        }
      })
      .catch(e => context.error(e))
  }
}
</script>

<style scoped>
.single-post-page {
  padding: 30px;
  text-align: center;
  box-sizing: border-box;
}

.post {
  width: 100%;
}

.post img {
  width: 70%;
  border-radius: 2px;
  margin: 5px 5px 30px 5px;
}

@media (min-width: 768px) {
  .post {
    width: 600px;
    margin: auto;
  }
}

.post-title {
  margin: 0;
}

.post-details {
  padding: 10px;
  box-sizing: border-box;
  border-bottom: 3px solid #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

@media (min-width: 768px) {
  .post-details {
    flex-direction: row;
  }
}

.post-detail {
  color: rgb(88, 88, 88);
  margin: 0 10px;
}

.post-feedback a {
  color: red;
  text-decoration: none;
}

.post-feedback a:hover,
.post-feedback a:active {
  color: salmon;
}
</style>
