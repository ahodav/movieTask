<template>
  <div class="container">
    <h3 class="title">
      Popular Movies
    </h3>
    <div class="list-card">
      <SingleFilm v-for="item in listOfMovies" :key="item.id" :item="item" />
    </div>
    <div class="mt-3">
      <b-pagination-nav v-model="page" :link-gen="linkGen" :number-of-pages="500" use-router align="center" />
    </div>
  </div>
</template>

<script>

import config from '../configMoveDB'

export default {
  async fetch () {
    if (this.$route.params.page >= 1) {
      this.page = this.$route.params.page
    }
    await this.$axios.get(`${config.url.popular}?api_key=${config.apiKey}&language=ru-RU&page=${this.page}`)
      .then((res) => {
        this.listOfMovies = res.data.results
      })
  },
  data () {
    return {
      listOfMovies: null,
      page: 1
    }
  },
  methods: {
    linkGen (pageNum) {
      return pageNum === 1 ? '/' : `${pageNum}`
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
