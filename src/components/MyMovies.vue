<template>
  <div class="container">
    <div class="search_bar">
      <input v-model="search" type="text" />
      <button @click="callApi(search)">Search</button>
    </div>
    <!-- /.search_bar -->
    <div class="movies">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <div class="jumbo_movie">
          <img
            :src="'http://image.tmdb.org/t/p/w300/' + movie.poster_path"
            alt=""
          />
        </div>
        <div class="specifications_movie">
          <h4>Title: {{ movie.title }} {{ movie.name }}</h4>
          <h5>
            Original title: {{ movie.original_title }} {{ movie.original_name }}
          </h5>
          <div class="languages">
            <p>Language:</p>
            <div class="flag">
              <img
                :src="movie.original_language"
                :alt="movie.original_language"
                width="25"
              />
            </div>
          </div>
          <!-- /.languages -->
          <p>Vote: {{ movie.vote_average }}</p>
        </div>
        <!-- /.specifications_movie -->
      </div>
      <!-- /.movie -->
      <h5>{{ problem }}</h5>
    </div>
    <!-- /.movies -->
  </div>
  <!-- /.container -->
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      search: "",
      movies: [],
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
      ],
      countryCode: "",
      status: "",
    };
  },
  methods: {
    getMovie(textInput) {
      this.search = textInput;
      // console.log(this.search)
    },
    callApi() {
      this.getMovie(this.search);
      axios
        // eslint-disable-next-line quotes
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=2c70cf7212141e650767768ea94e23e6&language=en-US&query=" +
            this.search +
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
            this.search
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
      this.search = "";
    },
    flagsLanguage(listOfFlags) {
      listOfFlags.forEach((flag) => {
        this.iconsNations(flag);
      });
      return listOfFlags;
    },
    iconsNations(icon) {
      this.flags.forEach((element) => {
        console.log(element);
        if (icon.original_language === element.chiave) {
          icon.original_language = element.image;
        }
      });
    },
  },
  /*  mounted: function () {
    this.flagsLanguage()
  } */
};
</script>

<style lang="scss">
.container {
  max-width: 1200px;
  margin: 2rem auto;
  .search_bar {
    display: flex;
    justify-content: center;
    input {
      margin-right: 1rem;
    }
  }
  .movie {
    width: calc(100% / 6);
    .languages {
      display: flex;
      align-items: center;
      & img {
        margin-left: 0.5rem;
      }
    }
  }

  .movies {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
  }
}
.jumbo_movie {
  width: 200px;
  img {
    width: 100%;
  }
}
</style>