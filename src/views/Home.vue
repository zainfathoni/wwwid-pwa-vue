<template>
  <div class="home">
    <img src="../assets/logo.png">
    <HelloWorld v-if="loading" msg="Welcome to Your Vue.js App"/>
    <ul v-else>
      <li v-for="article in articles" :key="article.guid">
        <preview :article="article" />
      </li>
    </ul>
  </div>
</template>

<script>
const API_URL =
  'https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Fmedium.com%2Ffeed%2Fwwwid'
const PARAGRAPH = /<p>.*.<\/p>\n</g

import HelloWorld from '@/components/HelloWorld.vue'
import Preview from '@/components/Preview.vue'

export default {
  name: 'home',
  components: {
    HelloWorld,
    Preview
  },
  data() {
    return {
      loading: true,
      articles: []
    }
  },
  mounted() {
    this.fetchArticles()
  },
  methods: {
    fetchArticles() {
      this.loading = true
      fetch(API_URL)
        .then(resp => resp.json())
        .then(data => {
          this.articles = data.items.map(item => {
            item.contentView = item.content
              .match(PARAGRAPH)
              .shift()
              .slice(0, -1)
            item.slug = item.link.split('/').pop()
            return item
          })
          this.loading = false
        })
    }
  }
}
</script>
