<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <SearchTab
    @moviesFound="getMovieList"
    @seriesFound="getSerieList"
    />

    <MovieList
    :moviesSearched="this.searchedMovies"
    :seriesSearched="this.searchedSeries"
    />
  </div>
</template>

<script>
import SearchTab from './components/SearchTab.vue'
import MovieList from './components/MovieList.vue'

export default {
  name: 'App',
  components: {
    SearchTab,
    MovieList
  },
  data() {
    return {
      searchedMovies: [],
      searchedSeries: []
    }
  },
  methods: {
    getMovieList(list) {
      this.searchedMovies = list
      console.log("Lista FILM in App", this.searchedMovies);
    },
    getSerieList(list) {
    this.searchedSeries = list
    console.log("Lista SERIE in App", this.searchedSeries);
    }
  }
}
</script>

<style lang="scss">

</style>
