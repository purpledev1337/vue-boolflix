<template>

    <ul>
        <li
        v-for="movieCard, i in moviesSearched"
        :key="100+i">
            <h1>{{ movieCard.title }}</h1>
            <h2>{{ movieCard.vote_average}}</h2>
            <h3>{{ movieCard.original_title }}</h3>
            <img v-if="movieCard.original_language === 'it'" src="../assets/Flag_ITA.png" :alt="movieCard.original_language">
            <img v-if="movieCard.original_language === 'en'" src="../assets/Flag_UK.png" :alt="movieCard.original_language">
            <img v-if="movieCard.original_language !== 'it' & movieCard.original_language !== 'en'" src="../assets/Flag_WORLD.jpg" :alt="movieCard.original_language">
        </li>
        <li
        v-for="serieCard, j in seriesSearched"
        :key="200+j">
            <h1>{{ serieCard.name }}</h1>
            <h2>{{ serieCard.vote_average}}</h2>
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
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

img {
    width: 30px;
}

</style>
