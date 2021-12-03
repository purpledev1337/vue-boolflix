<template>

    <ul>
        <li
        v-for="movieCard, i in moviesSearched"
        :key="'m'+ i">
            <img v-if="movieCard.poster_path !== null" class="poster_img" :src="posterUrl + movieCard.poster_path" :alt="movieCard.title">
            <img v-else src="../assets/Poster_NULL.jpg" class="poster_img" :alt="movieCard.name">
            <h1>{{ movieCard.title }}</h1>
            <h2>{{ movieCard.vote_average }}</h2>
            <span v-for="index in parseInt(Math.round(movieCard.vote_average / 2))" :key="movieCard.id + index">x</span>
            <span v-for="index in (5 - parseInt(Math.round(movieCard.vote_average / 2)))" :key="movieCard.id + 'empty' + index">o</span>
            <h3>{{ movieCard.original_title }}</h3>
            <img v-if="movieCard.original_language === 'it'" src="../assets/Flag_ITA.png" :alt="movieCard.original_language">
            <img v-if="movieCard.original_language === 'en'" src="../assets/Flag_UK.png" :alt="movieCard.original_language">
            <img v-if="movieCard.original_language !== 'it' & movieCard.original_language !== 'en'" src="../assets/Flag_WORLD.jpg" :alt="movieCard.original_language">
        </li>
        <li
        v-for="serieCard, j in seriesSearched"
        :key="'s'+ j">
            <img v-if="serieCard.poster_path !== null" class="poster_img" :src="posterUrl + serieCard.poster_path" :alt="serieCard.name">
            <img v-else src="../assets/Poster_NULL.jpg" class="poster_img" :alt="serieCard.name">
            <h1>{{ serieCard.name }}</h1>
            <h2>{{ serieCard.vote_average}}</h2>
            <font-awesome-icon icon="spinner" />
            <span v-for="index in parseInt(Math.round(serieCard.vote_average / 2))" :key="index + serieCard.id">x</span>
            <span v-for="index in (5 - parseInt(Math.round(serieCard.vote_average / 2)))" :key="serieCard.id + 'empty' + index">o</span>
            <h3>{{ serieCard.original_name }}</h3>
            <img v-if="serieCard.origin_country == 'IT'" src="../assets/Flag_ITA.png" :alt="serieCard.origin_country">
            <img v-if="serieCard.origin_country == 'GB'" src="../assets/Flag_UK.png" :alt="serieCard.origin_country">
            <img v-if="serieCard.origin_country == 'US'" src="../assets/Flag_US.png" :alt="serieCard.origin_country">
            <img v-if="serieCard.origin_country != 'IT' & serieCard.origin_country != 'GB' & serieCard.origin_country != 'US'" src="../assets/Flag_WORLD.jpg" :alt="serieCard.original_language">
        </li>
    </ul>

</template>

<script>

export default {
  name: 'MovieList',
  props: {
      moviesSearched : Array,
      seriesSearched : Array
  },
  data() {
      return {
          posterUrl : 'http://image.tmdb.org/t/p/w780/'
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

img {
    width: 30px;
}

.poster_img {
    width: 150px;
    height: 200px;
}
</style>
