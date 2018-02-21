<template>
  <section class="preview">
    <div class="img">
      <img :src="article.thumbnail" :alt="article.slug">
    </div>
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
