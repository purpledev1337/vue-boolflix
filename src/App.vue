<template>
  <div>
    <header>
      <img alt="BoolFlix logo" src="./assets/Netflix_logo.png">
      <SearchTab id="search_tab"
      @moviesFound="getMovieList"
      @seriesFound="getSerieList"
      @actorsFound="getActorsList"
      />
    </header>

    <main>
    <MovieList
    :moviesSearched="this.searchedMovies"
    :seriesSearched="this.searchedSeries"
    :actorsSearched="this.searchedActors"
    />
    </main>
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
      searchedSeries: [],
      searchedActors: []
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
    },
    getActorsList(list) {
      this.searchedActors = list
    console.log("Lista SERIE in App", this.searchedActors);
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

div {
  background-color: gray;
}

header {
  height: 150px;
  background-color: black;
  padding: 0 50px;
  display: flex;
  justify-content: space-between;
  align-items: center;

  img {
    height: 90%;
  }
}

main {
  height: 100%;
  background-color: gray;
}
</style>
