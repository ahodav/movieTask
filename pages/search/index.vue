<template>
  <div class="container">
    <h3 class="title">
      Search Movies
    </h3>
    <div class="list-card">
      <SingleFilm v-for="item in listOfMovies" :key="item.id" :item="item" />
    </div>
    <div class="mt-3">
      <b-pagination-nav v-model="page" :link-gen="linkGen" :number-of-pages="totalPages" use-router align="center" />
    </div>
  </div>
</template>

<script>

import config from '../../configMoveDB'

export default {
  async fetch () {
    if (this.$route.query.page) {
      this.page = this.$route.query.page
    }
    await this.$axios.get(`${config.url.search}?api_key=${config.apiKey}&language=ru-RU&query=${this.$route.query.query}&page=${this.page}&include_adult=false`)
      .then((res) => {
        this.listOfMovies = res.data.results
        this.totalPages = res.data.total_pages
        this.page = res.data.page
      })
  },
  data () {
    return {
      listOfMovies: null,
      page: 1,
      rows: 5,
      totalPages: null
    }
  },
  watch: {
    '$route.query': '$fetch'
  },
  methods: {
    linkGen (pageNum) {
      return `/search?query=${this.$route.query.query}&page=${pageNum}`
    }
  }
}
</script>

<style>
  .title {
    margin: 12px;
  }
  .list-card {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
</style>
