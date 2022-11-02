<template>


    <div id="list_container">
        <div :class="filterMovies()" class="card"
        v-for="movieCard, i in moviesSearched"
        :key="'m'+ i">
            <img class="poster_img" :src="getPosterImg(movieCard)" :alt="movieCard.title">
            <div class="info_container">
                <h1>{{ movieCard.title }}</h1>
                <h3 v-if="movieCard.title !== movieCard.original_title">({{ movieCard.original_title }})</h3>
                <div class="language_container">
                    Lingua:
                    <img class="flag" :src="pickMovieFlag(movieCard)" :alt="movieCard.original_language">
                </div>
                <div class="star_container">
                    Voto:
                    <font-awesome-icon icon="star" v-for="index in 5" :key="index" :class="star(index, movieCard.vote_average)" />
                    <h2>({{ movieCard.vote_average }})</h2>
                </div>
                <div class="main_actors">
                    <strong>Attori Principali: </strong>
                    <span class="actor_names" v-for="actor, k in movieCard.cast" :key="k">{{ actor.name }}, </span>
                </div>
                <p><strong>Trama: </strong>{{ movieCard.overview }}</p>
            </div>
        </div>
        <div :class="filterSeries()" class="card"
        v-for="serieCard, j in seriesSearched"
        :key="'s'+ j">
            <img class="poster_img" :src="getPosterImg(serieCard)">
            <div class="info_container">
                <h1>{{ serieCard.name }}</h1>
                <h3 v-if="serieCard.name !== serieCard.original_name">({{ serieCard.original_name }})</h3>
                <div class="language_container">
                    Paese di Produzione:
                    <img class="flag" :src="pickSerieFlag(serieCard)" :alt="serieCard.origin_country">
                </div>
                <div class="star_container">
                    Voto:
                    <font-awesome-icon icon="star" v-for="index in 5" :key="index" :class="star(index, serieCard.vote_average)" />
                    <h2>({{ serieCard.vote_average}})</h2>
                </div>
                <div class="main_actors">
                    <strong>Attori Principali: </strong>
                    <span class="actor_names" v-for="actor, l in serieCard.cast" :key="l">{{ actor.name }}, </span>
                </div>
                <p><strong>Trama: </strong>{{ serieCard.overview }}</p>
            </div>    
        </div>
        
    </div>

</template>

<script>

export default {
  name: 'MovieList',
  props: {
      moviesSearched : Array,
      seriesSearched : Array,
      filterTypeSelected : String,
      searchInput : String
  },
  data() {
      return {
          posterUrl: 'http://image.tmdb.org/t/p/w780/',
          flagIt: "https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Flag_of_Italy.svg/1200px-Flag_of_Italy.svg.png",
          flagUk: "https://upload.wikimedia.org/wikipedia/commons/8/83/Flag_of_the_United_Kingdom_%283-5%29.svg",
          flagUs: "https://upload.wikimedia.org/wikipedia/commons/e/e2/Flag_of_the_United_States_%28Pantone%29.svg",
          flagWorld: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/World_Flag_%282004%29.svg/800px-World_Flag_%282004%29.svg.png",
          movieClass: 'active',
          serieClass: 'active'
      }
  },
  methods: {
      star(index, value) {
          let vote = Math.round(value / 2);
          if (index <= vote) {
              return "active";
          }
      },
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
          } else {
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
      },
      filterMovies() {
        if (this.filterTypeSelected == 'both' | this.filterTypeSelected == 'movies') {
            return "visible"
        } if (this.filterTypeSelected == 'series') {
            return "not_visible"
        }
      },
      filterSeries() {
        if (this.filterTypeSelected == 'both' | this.filterTypeSelected == 'series') {
            return "visible"
            } if (this.filterTypeSelected == 'movies') {
            return "not_visible"
        }
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#list_container {
    display: flex;
    flex-wrap: wrap;
}

.card {
    width: calc(100% / 6 - 10px);
    height: 450px;
    margin: 2.5px 5px;
    background-color: rgb(30, 30, 30);
    color: white;
    border-radius: 15px;
    position: relative;
    transition: all ease-out 500ms;

    &:hover .poster_img {
        display: none;
        }

    &:hover {
        z-index: 1000;
        transform: scale(1.15);
    }

    .poster_img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        position: absolute;
        border-radius: 15px;

    }

    .info_container {
        height: 100%;
        display: flex;
        background-color: inherit;
        padding: 5px 20px;
        flex-direction: column;
        justify-content: flex-start;
        border-radius: 15px;


        h1 {
            margin: 15px 0;
            text-align: center;
            font-size: 1.5em;
        }

        h3 {
            margin: 15px 0;
        }

        .language_container {
            background-color: inherit;
            vertical-align: middle;
            line-height: 30px;

            .flag {
                width: 50px;
                height: 30px;
                margin-left: 10px;
                display: inline-block;
            }
        }

        .star_container {
            background-color: inherit;
            margin: 10px 0;

            .active {
                color: gold;
            }

            .inactive {
                color: grey;
            }

            h2 {
                margin-left: 5px;
                display: inline-block;
                font-size: 1em;
            }
        }

        .main_actors {
            background-color: inherit;
            margin-bottom: 10px;
        }

        p {
            width: 100%;
            height: 110px;
            white-space: wrap;
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 6;
            line-clamp: 6; 
            -webkit-box-orient: vertical;
        }
    }
}

.visible {
    display: block;
}

.not_visible {
    display: none;
}

.poster_img {
    width: 150px;
    height: 200px;
}
</style>
