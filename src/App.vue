<template>
  <div class="container pt-1">
    <div class="card">
      <h2>News {{ now }}</h2>
      <span> Open: <strong>{{ openRate }}</strong> | Read: <strong>{{ readRate }}</strong></span>
    </div>

  <app-news
    v-for="item in news"
    :key="item.id"
    :title="item.title"
    :id="item.id"
    :is-open="item.isOpen"
    :was-read="item.wasRead"
    @open-news="openNews"
    @read-news="readNews"
    @unmark="unreadNews">


  </app-news>

  </div>
</template>

<script>
import AppNews from './AppNews'


export default {
  data() {
    return {
      now: new Date().toLocaleDateString(),
      openRate: 0,
      readRate: 0,
      news: [
        {
          title: 'Joe Biden wins',
          id: 1,
          isOpen: false,
          wasRead: false
        },
        {
          title: 'Bitcoin now 40000$',
          id: 2,
          isOpen: false,
          wasRead: false
        }
      ]
    }
  },
   provide() {
    return {
      title: 'list of news',
      news: this.news
    }
  },
  methods: {
    openNews() {
      this.openRate++
    },
    readNews(id) {
      const idx = this.news.findIndex(news => news.id === id)
      this.news[idx].wasRead = true
      this.readRate++
    },
    unreadNews(id) {
      const news = this.news.find(news => news.id === id)
      news.wasRead = false
      this.readRate--
    }
  },
  components: {
    appNews: AppNews
  }
}

</script>

<style scoped>
  h2 {
    color:darkred
  }
</style>
