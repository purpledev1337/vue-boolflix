<template>
  <div>
    <input v-model="searchTxt" type="text">
    <button @click="searchMovie">Cerca</button>
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
      searchedMoviesList: []
    }
  },
  methods: {
    searchMovie() {
      this.apiUrl = "https://api.themoviedb.org/3/search/movie?api_key=6daf8c812c8d1160c91335b1fd6ab733&query=" + this.searchTxt.replace(/\s/g,"+");
      axios
      .get(this.apiUrl)
      .then((foundList) => {
        this.searchedMoviesList = foundList.data.results;
        console.log("Lista in SearchTab", this.searchedMoviesList);
        this.$emit('searchDone', this.searchedMoviesList)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
