<template>
  <div class="home">
    <img src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
const API_URL = 'https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Fmedium.com%2Ffeed%2Fwwwid'
const PARAGRAPH = /<p>.*.<\/p>\n</g

import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  },
  data() {
    return {
      loading: true,
      articles: []
    }
  },
  mounted () {
    this.fetchArticles()
  },
  methods: {
    fetchArticles() {
      this.loading = true
      fetch(API_URL)
      .then(resp => resp.json())
      .then(data => {
        this.articles = data.items.map(item => {
          item.contentView = item.content.match(PARAGRAPH).shift().slice(0, -1)
          item.slug = item.link.split('/').pop()
          return item
        })
        this.loading = false
      })
    }
  }
}
</script>
