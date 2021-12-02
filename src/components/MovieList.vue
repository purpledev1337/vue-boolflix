<template>

    <ul>
        <li
        v-for="movie, i in moviesSearched"
        :key="i">
            <h1>{{ movie.title }}</h1>
            <h2>{{ movie.vote_average}}</h2>
            <h3>{{ movie.original_title }}</h3>
            <img v-if="movie.original_language === 'it'" src="../assets/Flag_ITA.png" :alt="movie.original_language">
            <img v-if="movie.original_language === 'en'" src="../assets/Flag_UK.png" :alt="movie.original_language">
            <img v-if="movie.original_language !== 'it' & movie.original_language !== 'en'" class="world_flag" src="../assets/Flag_WORLD.jpg" :alt="movie.original_language">
        </li>
    </ul>

</template>

<script>

export default {
  name: 'MovieList',
  props: {
      moviesSearched : Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

img {
    width: 30px;
}

</style>
