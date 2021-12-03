<template>

    <ul>
        <li
        v-for="movieCard, i in moviesSearched"
        :key="'m'+ i">
            <img class="poster_img" :src="getPosterImg(movieCard)" :alt="movieCard.title">
            <h1>{{ movieCard.title }}</h1>
            <h2>{{ movieCard.vote_average }}</h2>
            <font-awesome-icon icon="star" class="filled_star" v-for="index in parseInt(Math.round(movieCard.vote_average / 2))" :key="movieCard.id + index"></font-awesome-icon>
            <font-awesome-icon icon="star" v-for="index in (5 - parseInt(Math.round(movieCard.vote_average / 2)))" :key="movieCard.id + 'empty' + index"></font-awesome-icon>
            <h3>{{ movieCard.original_title }}</h3>
            <img :src="pickMovieFlag(movieCard)" :alt="movieCard.original_language">
        </li>
        <li
        v-for="serieCard, j in seriesSearched"
        :key="'s'+ j">
            <img class="poster_img" :src="getPosterImg(serieCard)">
            <h1>{{ serieCard.name }}</h1>
            <h2>{{ serieCard.vote_average}}</h2>
            <font-awesome-icon icon="star" class="filled_star" v-for="index in parseInt(Math.round(serieCard.vote_average / 2))" :key="serieCard.id + index"></font-awesome-icon>
            <font-awesome-icon icon="star" v-for="index in (5 - parseInt(Math.round(serieCard.vote_average / 2)))" :key="serieCard.id + 'empty' + index"></font-awesome-icon>
            <h3>{{ serieCard.original_name }}</h3>
            <img :src="pickSerieFlag(serieCard)" :alt="serieCard.origin_country">
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
          posterUrl: 'http://image.tmdb.org/t/p/w780/',
          flagIt: "https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Flag_of_Italy.svg/1200px-Flag_of_Italy.svg.png",
          flagUk: "https://upload.wikimedia.org/wikipedia/commons/8/83/Flag_of_the_United_Kingdom_%283-5%29.svg",
          flagUs: "https://upload.wikimedia.org/wikipedia/commons/e/e2/Flag_of_the_United_States_%28Pantone%29.svg",
          flagWorld: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/World_Flag_%282004%29.svg/800px-World_Flag_%282004%29.svg.png"
      }
  },
  methods: {
      getPosterImg(arg) {
          if (arg.poster_path !== null) {
              return (this.posterUrl + arg.poster_path)
          } else {
              return "https://ih1.redbubble.net/image.460040615.2591/fposter,small,wall_texture,product,750x1000.u1.jpg"
          }
      },
      pickMovieFlag(arg) {
          if (arg.original_language === 'it') {
              return this.flagIt
          } if (arg.original_language === 'en' ) {
              return this.flagUk
          }  else {
              return this.flagWorld
          }
      },
      pickSerieFlag(arg) {
          if (arg.origin_country[0] === 'IT') {
              return this.flagIt
          } if (arg.origin_country[0] === 'GB') {
              return this.flagUk
          } if (arg.origin_country[0] === 'US') {
              return this.flagUs
          } else {
              return this.flagWorld
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

img {
    width: 50px;
    height: 30px;
}

.poster_img {
    width: 150px;
    height: 200px;
}

.filled_star {
    color: blue;
    filter: invert(1);
}
</style>
