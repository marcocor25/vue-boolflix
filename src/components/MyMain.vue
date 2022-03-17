<template>
  <!-- MAIN CONTAINER -->
  <div class="container">
    <!-- HEADER -->
    <div class="header">
      <!-- LOGO & CATEGORY WRAPPER -->
      <div class="logo-category-wrapper">
        <!-- LOGO -->
        <figure class="logo">
          <img src="../assets/img/logo.png" />
        </figure>
        <!-- LOGO SMALL -->
        <figure class="logo-small">
          <img src="../assets/img/logo-small.png" />
        </figure>
        <div class="category-box">
          <h3 @click="clickFilm()">Film</h3>
          <h3 @click="clickSerie()">Serie TV</h3>
        </div>
      </div>
      <!-- INPUT -->
      <div class="input-wrapper">
        <input
          type="search"
          placeholder="Cerca tra i film e le serie tv..."
          @keyup.enter="cercaFilm(), cercaSerie()"
          v-model="search"
        />
        <button @click="cercaFilm(), cercaSerie()">Cerca</button>
      </div>
    </div>
    <!-- CONTAINER LISTE -->
    <ul class="list-container">
      <!-- DEFAULT MESSAGE -->
      <div class="default" v-if="movies == '' && tvSerires == ''">
        <h1>Benvenuto su Netflix!</h1>
        <p>Effettua una ricerca per cominciare.</p>
      </div>
      <!-- CATEGORY - FILM -->
      <div class="category" v-if="movies != ''">
        <h1>Film</h1>
      </div>
      <!-- LISTA FILM -->
      <li v-for="movie in movies" :key="movie.id">
        <!-- COPERTINA FILM -->
        <img
          :src="`https://image.tmdb.org/t/p/w342${movie.poster_path}`"
          :alt="movie.title"
        />
        <!-- INFO-BOX IN HOVER -->
        <div class="hover-info">
          <!-- WRAPPER TITOLI FILM -->
          <div class="title-wrapper">
            <!-- TITOLO -->
            <h3>{{ movie.title }}</h3>
            <!-- BADGE -->
            <span class="badge">Film</span>
          </div>
          <!-- INFO-BOX -->
          <div class="info-box">
            <p><strong>Titolo originale: </strong>{{ movie.original_title }}</p>
            <p v-if="movie.original_language == 'it'">Lingua originale: 🇮🇹</p>
            <p v-else-if="movie.original_language == 'fr'">
              <strong>Lingua originale: </strong>🇫🇷
            </p>
            <p v-else-if="movie.original_language == 'es'">
              <strong>Lingua originale: </strong>🇪🇸
            </p>
            <p v-else-if="movie.original_language == 'en'">
              <strong>Lingua originale: </strong>🇬🇧
            </p>
            <p v-else-if="movie.original_language == 'de'">
              <strong>Lingua originale: </strong>🇩🇪
            </p>
            <p v-else>
              <strong>Lingua originale: </strong>{{ movie.original_language }}
            </p>
            <!-- STELLE VOTI -->
            <div class="votes">
              <strong>Voto: </strong>
              <p
                :class="i < catchVoteMovie(movie) ? 'stars' : ''"
                v-for="(element, i) in 5"
                :key="i"
              >
                &starf;
              </p>
            </div>
            <!-- OVERVIEW -->
            <p>
              <strong>Trama: </strong>
              <span v-if="movie.overview == ''">n/d</span>
              {{ movie.overview }}
            </p>
          </div>
        </div>
      </li>
      <!-- CATEGORY - SERIE TV -->
      <div class="category" v-if="tvSerires != ''">
        <h1>Serie TV</h1>
      </div>
      <!-- LISTA SERIE -->
      <li v-for="series in tvSerires" :key="series.id">
        <!-- COPERTINA SERIE -->
        <img
          :src="`https://image.tmdb.org/t/p/w342${series.poster_path}`"
          :alt="series.name"
        />
        <!-- INFO-BOX IN HOVER -->
        <div class="hover-info">
          <!-- WRAPPER TITOLI SERIE TV -->
          <div class="title-wrapper">
            <!-- TITOLO -->
            <h3>{{ series.name }}</h3>
            <!-- BADGE -->
            <span class="badge">Serie TV</span>
          </div>
          <!-- INFO-BOX -->
          <div class="info-box">
            <p><strong>Titolo originale: </strong>{{ series.original_name }}</p>
            <p v-if="series.original_language == 'it'">Lingua originale: 🇮🇹</p>
            <p v-else-if="series.original_language == 'fr'">
              <strong>Lingua originale: </strong>🇫🇷
            </p>
            <p v-else-if="series.original_language == 'es'">
              <strong>Lingua originale: </strong>🇪🇸
            </p>
            <p v-else-if="series.original_language == 'en'">
              <strong>Lingua originale: </strong>🇬🇧
            </p>
            <p v-else-if="series.original_language == 'de'">
              <strong>Lingua originale: </strong>🇩🇪
            </p>
            <p v-else>
              <strong>Lingua originale: </strong>{{ series.original_language }}
            </p>
            <!-- STELLE VOTI -->
            <div class="votes">
              <strong>Voto: </strong>
              <p
                :class="i < catchVoteSeries(series) ? 'stars' : ''"
                v-for="(element, i) in 5"
                :key="i"
              >
                &starf;
              </p>
            </div>
            <!-- OVERVIEW -->
            <p>
              <strong>Trama: </strong>
              <span v-if="series.overview == ''">n/d</span>
              {{ series.overview }}
            </p>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "MyMain",
  data() {
    return {
      baseURL: "https://api.themoviedb.org/3",
      search: "",
      movies: [],
      tvSerires: [],
    };
  },
  methods: {
    cercaFilm: function () {
      axios
        .get(`${this.baseURL}/search/movie`, {
          params: {
            api_key: "9857cfb37fc41b760e69c70f6d75b517",
            query: this.search,
            language: "it-IT",
          },
        })
        .then((res) => {
          this.movies = res.data.results;
          this.search = "";
        })
        .catch((err) => {
          console.log(err.response);
        });
    },

    cercaSerie: function () {
      axios
        .get(`${this.baseURL}/search/tv`, {
          params: {
            api_key: "9857cfb37fc41b760e69c70f6d75b517",
            query: this.search,
            language: "it-IT",
          },
        })
        .then((res) => {
          this.tvSerires = res.data.results;
          this.search = "";
        })
        .catch((err) => {
          console.log(err.response);
        });
    },

    clickFilm: function () {
      axios
        .get(`${this.baseURL}/search/movie`, {
          params: {
            api_key: "9857cfb37fc41b760e69c70f6d75b517",
            query: "marvel",
            language: "it-IT",
          },
        })
        .then((res) => {
          this.movies = res.data.results;
          this.tvSerires.splice(this.tvSerires);
        })
        .catch((err) => {
          console.log(err.response);
        });
    },

    clickSerie: function () {
      axios
        .get(`${this.baseURL}/search/tv`, {
          params: {
            api_key: "9857cfb37fc41b760e69c70f6d75b517",
            query: "casa",
            language: "it-IT",
          },
        })
        .then((res) => {
          this.tvSerires = res.data.results;
          this.movies.splice(this.movies);
        })
        .catch((err) => {
          console.log(err.response);
        });
    },

    catchVoteMovie: function (movie) {
      return Math.ceil(movie.vote_average / 2);
    },

    catchVoteSeries: function (series) {
      return Math.ceil(series.vote_average / 2);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  display: flex;
  flex-direction: column;

  .header {
    min-height: 60px;
    padding: 0 40px;
    display: flex;
    align-items: center;
    position: sticky;
    top: 0;
    left: 0;
    z-index: 1;
    box-shadow: 1px 1px 3px #000000;
    background: #0a0a0a;

    .logo-category-wrapper {
      flex-grow: 1;
      display: flex;
      align-items: center;
      gap: 40px;

      .logo {
        width: 100px;
      }

      .logo-small {
        display: none;
        width: 70px;
      }

      .category-box {
        display: flex;
        gap: 20px;

        h3 {
          font-weight: lighter;
          cursor: pointer;
          color: #c1c1c1;

          &:hover {
            color: currentColor;
            text-decoration: underline;
          }
        }
      }
    }

    .input-wrapper {
      width: 350px;
      height: 30px;
      display: flex;
      gap: 10px;

      input {
        width: 100%;
        padding: 0 5px;
        border-radius: 5px;
        border: 1px solid #555;
        color: currentColor;
        background: transparent;

        &:focus-visible {
          outline: none;
        }
      }

      button {
        padding: 0 10px;
        border-radius: 5px;
        border: 1px solid #555;
        color: currentColor;
        background: transparent;
      }
    }
  }

  .list-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 15px;
    padding: 0 30px;
    padding-bottom: 30px;

    .category,
    .default {
      width: 100%;
      padding: 0 10px;
      padding-top: 30px;
      font-size: 20px;
    }

    .default {
      color: #c1c1c1;

      h1 {
        filter: drop-shadow(4px 4px 1px #0a0a0a);
        color: #ff1a0c;
      }
    }

    li {
      width: calc((100% / 5) - 15px);
      min-height: 400px;
      border: 0.1px solid #555;
      cursor: pointer;
      background-color: #0a0a0a;
      background-image: url(../assets/img/logo-small.png);
      background-position: center;
      background-size: contain;
      background-repeat: no-repeat;
      transition: 200ms linear;
      position: relative;

      img {
        object-fit: cover;
        object-position: center;
      }

      &:hover {
        transform: scale(0.97);
      }

      .hover-info {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        padding: 10px;
        opacity: 0;
        background: rgba($color: #000000, $alpha: 0.8);
        overflow: auto;
        transition: 200ms linear;
      }

      &:hover .hover-info {
        opacity: 1;
      }

      .title-wrapper {
        padding: 20px 0;
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 20px;
        border-bottom: 1px solid #ff1a0c;

        .badge {
          flex-shrink: 0;
          padding: 0 5px;
          font-size: 12px;
          border-radius: 5px;
          background: #ff1a0c;
        }
      }

      .info-box {
        line-height: 22px;
        padding-top: 10px;
        overflow: auto;
      }

      .votes {
        display: flex;
        align-items: baseline;
        gap: 3px;

        .stars {
          color: #ff1a0c;
        }
      }
    }
  }
}

// VIEWPORT:

// LARGE
@media all and (max-width: 992px) {
  li {
    width: calc((100% / 3) - 15px) !important;
  }
}

// MEDIUM
@media all and (max-width: 768px) {
  li {
    width: calc((100% / 2) - 15px) !important;
  }

  .input-wrapper {
    width: 220px !important;
  }
}

// SMALL
@media all and (max-width: 576px) {
  li {
    width: calc((100% / 1) - 15px) !important;
  }

  .logo-category-wrapper {
    gap: 10px !important;

    .logo {
      display: none;
    }

    .logo-small {
      display: block !important;
    }
  }

  .input-wrapper {
    width: 160px !important;

    button {
      display: none;
    }
  }
}
</style>
