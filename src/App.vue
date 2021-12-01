<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <SearchTab
    @searchDone="getMovieList"
    />

    <MovieList
    :moviesSearched="this.searchedMovies"
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
      searchedMovies: []
    }
  },
  methods: {
    getMovieList(list) {
      this.searchedMovies = list
      console.log("Lista in App", this.searchedMovies);
    }
  }
}
</script>

<style lang="scss">

</style>
