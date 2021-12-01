<template>

    <ul>
        <li
        v-for="movie, i in moviesSearched"
        :key="i">
            <h1>{{ movie.title }}</h1>
            <h2>{{ movie.vote_average}}</h2>
            <h3>{{ movie.original_title }}</h3>
            <h4>{{ movie.original_language }}</h4>
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

</style>
