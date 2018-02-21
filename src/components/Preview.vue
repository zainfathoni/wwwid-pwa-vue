<template>
  <section class="preview">
    <div class="img">
      <img :src="article.thumbnail" :alt="article.slug">
    </div>
    <h1 class="title">{{ article.title }}</h1>
    <div class="meta">
      <span class="author">{{ article.author }}</span>
      <span class="date">{{ article.pubDate }}</span>
    </div>
    <div class="content" v-html="article.preview"/>
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
