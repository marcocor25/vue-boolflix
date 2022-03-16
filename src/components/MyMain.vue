<template>
  <!-- MAIN CONTAINER -->
  <div class="container">
    <div class="header">
      <!-- LOGO -->
      <figure class="logo">
        <img src="../assets/img/Boolflix.svg" />
      </figure>
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
    padding: 0 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: sticky;
    top: 0;
    left: 0;
    z-index: 1;
    background: #0a0a0a;

    .logo {
      width: 100px;
    }

    .input-wrapper {
      width: 30vw;
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
    padding: 30px;

    li {
      width: calc((100% / 5) - 15px);
      min-height: 400px;
      border: 1px solid #555;
      cursor: pointer;
      background-image: url(../assets/img/not-found.png);
      background-position: center;
      background-size: cover;
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
        transition: 200ms linear;
      }

      &:hover .hover-info {
        opacity: 1;
      }

      .title-wrapper {
        height: 55px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 3px;
        border-bottom: 1px solid #d81f26;

        .badge {
          flex-shrink: 0;
          padding: 0 5px;
          font-size: 12px;
          border-radius: 5px;
          user-select: none;
          background: #d81f26;
        }
      }

      .info-box {
        height: calc(100% - 55px);
        padding-top: 5px;
        overflow: auto;
      }

      .votes {
        display: flex;
        align-items: baseline;
        gap: 3px;

        .stars {
          color: #d81f26;
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
}

// SMALL
@media all and (max-width: 576px) {
  li {
    width: calc((100% / 1) - 15px) !important;
  }
}
</style>
