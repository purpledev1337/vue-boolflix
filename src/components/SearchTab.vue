<template>
  <div>
    <input v-model="searchTxt" type="text">
    <button @click="searchAny">Cerca</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'SearchTab',
  data() {
    return {
      searchTxt: '',
      apiUrl: '',
      searchedMoviesList: [],
      searchedSeriesList: []
    }
  },
  methods: {
    searchAny() {
      this.apiUrl = "https://api.themoviedb.org/3/search/movie?api_key=6daf8c812c8d1160c91335b1fd6ab733" + "&language=it-IT" + "&query=" + this.searchTxt.replace(/\s/g,"+");
      axios
      .get(this.apiUrl)
      .then((foundMoviesList) => {
          this.searchedMoviesList = foundMoviesList.data.results;
          console.log("Lista FILM in SearchTab", this.searchedMoviesList);
          this.$emit('moviesFound', this.searchedMoviesList);
          });
      this.apiUrl = "https://api.themoviedb.org/3/search/tv?api_key=6daf8c812c8d1160c91335b1fd6ab733" + "&language=it-IT" + "&query=" + this.searchTxt.replace(/\s/g,"+");
      axios
      .get(this.apiUrl)
      .then((foundSeriesList) => {
          this.searchedSeriesList = foundSeriesList.data.results;
          console.log("Lista SERIE in SearchTab", this.searchedSeriesList);
          this.$emit('seriesFound', this.searchedSeriesList)
          });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
