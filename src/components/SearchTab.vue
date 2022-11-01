<template>
  <div>
    <input v-model="searchTxt" @keyup.enter="searchAny" type="text">

    <select v-model="filterTypeSelected" name="filterType" id="0">
      <option value="both">Film e Serie Tv</option>
      <option value="movies">...solo Film</option>
      <option value="series">...solo Serie TV</option>
    </select>

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
      baseUrl: 'https://api.themoviedb.org/3/search/',
      apiKey: 'api_key=6daf8c812c8d1160c91335b1fd6ab733',
      apiLanguage: '&language=it-IT&query=',
      apiUrl: '',
      apiCreditsUrl: '',
      movieId: '',
      serieId: '',
      searchedMoviesList: [],
      searchedSeriesList: [],
      filterTypeSelected: 'both'
    }
  },
  methods: {
    searchAny() {
      this.$emit('filterTypeFound', this.filterTypeSelected)

      this.apiUrl = this.baseUrl + "movie?" + this.apiKey + this.apiLanguage + this.searchTxt.replace(/\s/g,"+");

      axios
      .get(this.apiUrl)
      .then((foundMoviesList) => {
          this.searchedMoviesList = foundMoviesList.data.results;
          this.searchedMoviesList.forEach((item) => {
            this.movieId = item.id
            this.apiCreditsUrl = 'https://api.themoviedb.org/3/movie/' + this.movieId + '/credits?api_key=6daf8c812c8d1160c91335b1fd6ab733';
            axios
            .get(this.apiCreditsUrl)
            .then((foundCreditsList) => {
              if (foundCreditsList.data.cast.length > 5) {
                foundCreditsList.data.cast.length = 5
              }
              // item.cast = foundCreditsList.data.cast
              this.$set(item, 'cast', foundCreditsList.data.cast);
            })
          });

          this.$emit('moviesFound', this.searchedMoviesList);
      });

      this.apiUrl = this.baseUrl + "tv?" + this.apiKey + this.apiLanguage + this.searchTxt.replace(/\s/g,"+");

      axios
      .get(this.apiUrl)
      .then((foundSeriesList) => {
        this.searchedSeriesList = foundSeriesList.data.results;
          this.searchedSeriesList.forEach((item) => {
            this.serieId = item.id
            this.apiCreditsUrl = 'https://api.themoviedb.org/3/tv/' + this.serieId + '/credits?api_key=6daf8c812c8d1160c91335b1fd6ab733';
            axios
            .get(this.apiCreditsUrl)
            .then((foundCreditsList) => {
              if (foundCreditsList.data.cast.length > 5) {
                foundCreditsList.data.cast.length = 5
              }
              this.$set(item, 'cast', foundCreditsList.data.cast);
            })
          })

          this.$emit('seriesFound', this.searchedSeriesList);
      });
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
div {
  background-color: black;
}

input[type=text] {
  width: 300px;
  height: 35px;
  padding: 15px;
  background-color: black;
  color: white;
  border: solid 3px black;
  border-bottom: 2px solid red;
}

button, select {
  width: 100px;
  height: 40px;
  border-radius: 5px;
  margin: 0 25px;
  border: none;
  color: white;
  font-size: 1.2em;
  background-color: red;
}

select {
  width: initial;
  background-color: black
}

</style>
