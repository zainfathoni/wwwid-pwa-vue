<template>
  <section class="preview">
    <div class="img">
      <img :src="article.thumbnail" :alt="article.slug">
    </div>
    <h1 class="title c">{{ article.title }}</h1>
    <div class="meta c">
      <span class="author">{{ article.author }}</span>
      <span class="date">{{ article.pubDate }}</span>
    </div>
    <div class="content c" v-html="article.preview"/>
  </section>
</template>

<script>
export default {
  props: {
    article: {
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.img > img {
  width: 100%;
  height: auto;
}
.img > img[lazy='loading'] {
  max-height: 200px;
}
.title {
  margin: 0.5em 0 1em;
  font-size: 1em;
  font-weight: 500;
}
.meta {
  margin-bottom: 1em;
}
.author,
.date {
  color: #ccc;
  font-size: 0.7em;
}
.author {
  float: left;
}
.date {
  float: right;
}
.content {
  font-size: 0.7em;
  color: #6d6565;
}
</style>
