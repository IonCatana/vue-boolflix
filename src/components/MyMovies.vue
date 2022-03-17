<template>
  <div>
    <header id="site_header">
      <div class="container">
        <div class="logo">
          <div class="hover_animation">
            <h2>BOOLFLIX</h2>
            <p>By Ion Catana with <span>&#10084;</span></p>
            <img src="../assets/img/bg-animation.gif" alt="" />
          </div>
          <SearchBar @searchMovies="getMovie" />
        </div>
      </div>
      <!-- /.container -->
    </header>    
    <!-- /#site_header -->
    <main id="site_main">
      <div class="container">
        <div class="movies_series">
          <div class="movie" v-for="movie in movies" :key="movie.id">
            <div class="jumbo" v-if="movie.poster_path !== null">
              <img
                class="poster"
                :src="'http://image.tmdb.org/t/p/w342' + movie.poster_path"
                :alt="movie.name"
              />
              <div class="info">
                <div class="specifications">
                  <h1>Movie</h1>
                  <h3>Title: {{ movie.title }}</h3>
                  <h4>Original title: {{ movie.original_title }}</h4>
                  <div class="languages">
                    <p><strong>Language: </strong></p>
                    <div class="flag">
                      <img
                        class="icon_flag"
                        :src="movie.original_language"
                        :alt="movie.original_language"
                        width="25"
                      />
                    </div>
                  </div>
                  <!-- /.languages -->
                  <div v-if="movie.vote_average >= 1">
                    <p>
                      <strong>Vote: </strong>d
                      <i
                        class="stars"
                        :class="classStars"
                        v-for="index in movie.vote_average"
                        :key="index.id"
                      ></i>
                    </p>
                  </div>
                  <div v-else>
                    <p><strong> Vote: </strong>{{ movie.vote_average }}</p>
                  </div>
                  <p v-if="movie.overview !== ''">
                    <strong>Overview:</strong> {{ movie.overview }}
                  </p>
                </div>
                <!-- /.specifications -->
              </div>
              <!-- /.info -->
            </div>
            <div v-else class="jumbo">
              <h3 class="avaiable">IMAGE NOT AVAIABLE</h3>
              <div class="info">
                <div class="specifications">                  
                  <h3>Title: {{ movie.title }}</h3>
                  <h4>Original title: {{ movie.original_title }}</h4>
                  <div class="languages">
                    <p><strong>Language: </strong></p>
                    <div class="flag">
                      <img
                        class="icon_flag"
                        :src="movie.original_language"
                        :alt="movie.original_language"
                        width="25"
                      />
                    </div>
                  </div>
                  <!-- /.languages -->
                  <div v-if="movie.vote_average >= 1">
                    <p>
                      <strong>Vote: </strong>
                      <i
                        class="stars"
                        :class="classStars"
                        v-for="index in movie.vote_average"
                        :key="index.id"
                      ></i>
                    </p>
                  </div>
                  <div v-else>
                    <p><strong>Vote: </strong> {{ movie.vote_average }}</p>
                  </div>
                  <p v-if="movie.overview !== ''">
                    <strong>Overview:</strong> {{ movie.overview }}
                  </p>
                </div>
                <!-- /.specifications -->
              </div>
            </div>
            <!-- /.jumbo -->
          </div>
          <!-- /.movie -->
          <div class="serie" v-for="serie in series" :key="serie.id">
            <div class="jumbo" v-if="serie.poster_path !== null">
              <img
                class="poster"
                :src="'http://image.tmdb.org/t/p/w342' + serie.poster_path"
                :alt="serie.name"
              />
              <div class="info">                
                <div class="specifications">
                  <h1>Serie</h1>
                  <h3>Title: {{ serie.name }}</h3>
                  <h4>Original title: {{ serie.original_name }}</h4>
                  <div class="languages">
                    <p><strong>Language: </strong></p>
                    <div class="flag">
                      <img
                        class="icon_flag"
                        :src="serie.original_language"
                        :alt="serie.original_language"
                        width="25"
                      />
                    </div>
                  </div>
                  <!-- /.languages -->
                  <div v-if="serie.vote_average >= 1">
                    <p>
                      <strong>Vote: </strong>
                      <i
                        class="stars"
                        :class="classStars"
                        v-for="index in serie.vote_average"
                        :key="index.id"
                      ></i>
                    </p>
                  </div>
                  <div v-else>
                    <p><strong> Vote: </strong>{{ serie.vote_average }}</p>
                  </div>
                  <p v-if="serie.overview !== ''">
                    <strong>Overview:</strong> {{ serie.overview }}
                  </p>
                </div>
                <!-- /.specifications -->
              </div>
            </div>
            <div v-else class="jumbo">
              <h3 class="avaiable">IMAGE NOT AVAIABLE</h3>
              <div class="info">
                <div class="specifications">
                  <h3>Title: {{ serie.name }}</h3>
                  <h4>Original title: {{ serie.original_name }}</h4>
                  <div class="languages">
                    <p><strong>Language: </strong></p>
                    <div class="flag">
                      <img
                        class="icon_flag"
                        :src="serie.original_language"
                        :alt="serie.original_language"
                        width="25"
                      />
                    </div>
                  </div>
                  <!-- /.languages -->
                  <div v-if="serie.vote_average >= 1">
                    <p>
                      <strong>Vote: </strong>
                      <i
                        class="stars"
                        :class="classStars"
                        v-for="index in serie.vote_average"
                        :key="index.id"
                      ></i>
                    </p>
                  </div>
                  <div v-else>
                    <p><strong>Vote: </strong> {{ serie.vote_average }}</p>
                  </div>
                  <p v-if="serie.overview !== ''">
                    <strong>Overview:</strong> {{ serie.overview }}
                  </p>
                </div>
                <!-- /.specifications -->
              </div>
            </div>
            <!-- /.jumbo -->
          </div>
          <!-- /.serie -->
          <h5>{{ problem }}</h5>
        </div>
        <!-- /.movies_series -->
      </div>
      <!-- /.container -->
    </main>
    <!-- /#site_main -->
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "../components/SearchBar.vue";
/* import SiteHeader from '../components/SiteHeader.vue' */
export default {
  components: {
    SearchBar,
  },
  data() {
    return {
      movies: [],
      series: [],
      problem: "",
      flags: [
        {
          chiave: "en",
          image: "https://images.emojiterra.com/twitter/512px/1f1ec-1f1e7.png",
        },
        {
          chiave: "it",
          image: "https://images.emojiterra.com/twitter/512px/1f1ee-1f1f9.png",
        },
        {
          chiave: "de",
          image:
            "https://images.emojiterra.com/twitter/v13.1/512px/1f1e9-1f1ea.png",
        },
        {
          chiave: "es",
          image:
            "https://images.emojiterra.com/twitter/v13.1/512px/1f1ea-1f1f8.png",
        },
        {
          chiave: "fr",
          image:
            "https://images.emojiterra.com/twitter/v13.1/512px/1f1eb-1f1f7.png",
        },
        {
          chiave: "ru",
          image:
            "https://images.emojiterra.com/twitter/v13.1/512px/1f1f7-1f1fa.png",
        },
        {
          chiave: "pt",
          image:
            "https://images.emojiterra.com/twitter/v13.1/512px/1f1f5-1f1f9.png",
        },
      ],
      countryCode: "",
      status: "",
      classStars: "fas fa-star",
      digitText: "",
    };
  },
  methods: {
    getMovie(textInput) {
      this.digitText = textInput;
      console.log(this.digitText);
      this.callApi();
    },
    callApi() {
      axios
        // eslint-disable-next-line quotes
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=2c70cf7212141e650767768ea94e23e6&language=en-US&query=" +
            this.digitText +
            "&page=1&include_adult=false"
        )
        .then((response) => {
          // console.log(response)
          this.movies = response.data.results;
          this.flagsLanguage(this.movies);
        })
        .catch((error) => {
          // console.log(error)
          this.problem = error;
          this.movies = "";
          console.log(this.problem);
        });
      axios
        // eslint-disable-next-line quotes
        .get(
          "https://api.themoviedb.org/3/search/tv?api_key=2c70cf7212141e650767768ea94e23e6&language=en-US&page=1&include_adult=false&query=" +
            this.digitText
        )
        .then((response) => {
          // console.log(response)
          this.series = response.data.results;
          this.flagsLanguage(this.series);
        })
        .catch((error) => {
          // console.log(error)
          this.problem = error;
          this.series = "";
          console.log(this.problem);
        });
    },
    resetText() {
      this.digitText = "";
      console.log(this.digitText);
    },
    flagsLanguage(listOfFlags) {
      listOfFlags.forEach((flag) => {
        this.iconsNations(flag);
        this.changeVotes(flag);
      });
      return listOfFlags;
    },
    iconsNations(icon) {
      this.flags.forEach((element) => {
        // console.log(element)
        if (icon.original_language === element.chiave) {
          icon.original_language = element.image;
        }
      });
    },
    changeVotes(item) {
      item.vote_average = Math.round(item.vote_average);
      if (item.vote_average === 10 || item.vote_average === 9) {
        item.vote_average = 5;
      } else if (item.vote_average === 8 || item.vote_average === 7) {
        item.vote_average = 4;
      } else if (item.vote_average === 6 || item.vote_average === 5) {
        item.vote_average = 3;
      } else if (item.vote_average === 4 || item.vote_average === 3) {
        item.vote_average = 2;
      } else if (item.vote_average === 2 || item.vote_average === 1) {
        item.vote_average = 1;
      }
    },
  },
  /*  mounted: function () {
    this.flagsLanguage()
  } */
};
</script>

<style lang="scss">
header {
  height: 100px;
  background-color: #000;
  .logo {
    h2 {
      color: red;
      position: absolute;
      transform: translate(-5%, 0%);
      font-size: 32px;
    }
    p {
      color: white;
      position: absolute;
      transform: translate(63%, 150%);
      font-size: 8px;
      text-align: center;
      span {
        color: red;
      }
    }
  }
}
#site_main {
  .movies_series {
    display: flex;
    flex-wrap: wrap;

    .movie,
    .serie {
      padding: 1rem;
      width: calc(100% / 3);
      height: 650px;
      margin-top: 1rem;
      .jumbo {
        height: 100%;
        border: 1px solid black;
        position: relative;
        transition: 500ms linear;
        &:hover {
          transform: scale(1.01);
          transition: 5000ms linear;
        }
        
        .avaiable {
          text-align: center;
          vertical-align: middle;
          line-height: 500px;
        }
      }
      .jumbo:hover .info {
        visibility: visible;
        cursor: pointer;
        opacity: 0.9;
        transform: scale(1.01);
        transition: 500ms linear;
      }
      .poster {
        height: 100%;
        width: 100%;
        object-fit: cover;
        display: block;
      }
      .info {
        visibility: hidden;
        height: calc(100% - 83.89px);
        border: 1px solid black;
        width: 100%;
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        background-color: #000;
        overflow: auto;
        .specifications {
          color: #fff;
          padding: 1rem;
          h1{
            padding-right: 5px;
            display: flex;
            justify-content: flex-end;
            display: block;
            color: red;
            text-align: right;
            background-color: orange;
          }
        }
      }
      .languages {
        display: flex;
        align-items: center;
        .icon_flag {
          margin-left: 0.5rem;
        }
      }
      .stars {
        color: gold;
      }
    }
  }
}
.hover_animation {
  width: 130px;
  height: 100px;
  background-repeat: no-repeat;
  background-position: center;
  object-fit: contain;
  img {
    width: 100%;
    margin-left: 15px;
  }
  display: flex;
  align-items: center;
  &:hover {
    cursor: pointer;
  }
}
</style>