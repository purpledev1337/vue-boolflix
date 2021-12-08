<template>

    <div id="list_container">
        <div class="card"
        v-for="movieCard, i in moviesSearched"
        :key="'m'+ i">
            <img class="poster_img" :src="getPosterImg(movieCard)" :alt="movieCard.title">
            <div class="info_container">
                <h1>{{ movieCard.title }}</h1>
                <h3 v-if="movieCard.title !== movieCard.original_title"><strong>Titolo Originale:</strong> {{ movieCard.original_title }}</h3>
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
                    <span><strong>Attori Principali:</strong> {{ printActors(i, 0) }}, {{ printActors(i, 1) }}, {{ printActors(i, 2) }}, {{ printActors(i, 3) }}, {{ printActors(i, 4) }}</span>
                </div>
                <p><strong>Trama: </strong>{{ movieCard.overview }}</p>
            </div>
        </div>
        <div class="card"
        v-for="serieCard, j in seriesSearched"
        :key="'s'+ j">
            <img class="poster_img" :src="getPosterImg(serieCard)">
            <div class="info_container">
                <h1>{{ serieCard.name }}</h1>
                <h3 v-if="serieCard.name !== serieCard.original_name">Titolo Originale: {{ serieCard.original_name }}</h3>
                <div class="language_container">
                    Paese di Produzione:
                    <img class="flag" :src="pickSerieFlag(serieCard)" :alt="serieCard.origin_country">
                </div>
                <div class="star_container">
                    Voto:
                    <font-awesome-icon icon="star" v-for="index in 5" :key="index" :class="star(index, serieCard.vote_average)" />
                    <h2>({{ serieCard.vote_average}})</h2>
                </div>
                <p><strong>Trama: </strong>{{ serieCard.overview }}</p>
            </div>    
        </div>
    </div>

</template>

<script>

export default {
  name: 'MovieList',
  actorsList: [],
  props: {
      moviesSearched : Array,
      seriesSearched : Array,
      actorsSearched : Array
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
      printActors(index, i) {
        //   for (let i = 0; i < 5; i++){
            if (this.actorsSearched[index].length > i) {
                return this.actorsSearched[index][i].name
            }
        //   }
      }
    //   getActors (movieId) {

    //     // for (let i = 0; i < this.moviesSearched.length; i++) {
    //         this.apiCreditsUrl = 'https://api.themoviedb.org/3/movie/' + movieId + '/credits?api_key=6daf8c812c8d1160c91335b1fd6ab733';

    //         axios
    //         .get(this.apiCreditsUrl)
    //         .then((foundCreditsList) => {
    //             let searchedCastList = foundCreditsList.data.cast
    //                 console.log("searchedCastList", searchedCastList);
    //                 searchedCastList.splice(5);
    //                 this.actorsList = searchedCastList
    //             // for (let j = 0; j < searchedCastList.length; j++) {
    //             //     let actorFound = searchedCastList[j].name
    //             //     console.log("attore trovato", actorFound);
    //             //     this.actorsList.push(actorFound)
    //             // }
    //         })
    //         .catch((error) => {
    //             console.log(error);
    //         })
    //     // }
    // }
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

.poster_img {
    width: 150px;
    height: 200px;
}
</style>
