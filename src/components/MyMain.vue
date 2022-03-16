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
            <p>Titolo originale: {{ movie.original_title }}</p>
            <p v-if="movie.original_language == 'it'">Lingua originale: 🇮🇹</p>
            <p v-else-if="movie.original_language == 'fr'">
              Lingua originale: 🇫🇷
            </p>
            <p v-else-if="movie.original_language == 'es'">
              Lingua originale: 🇪🇸
            </p>
            <p v-else-if="movie.original_language == 'en'">
              Lingua originale: 🇬🇧
            </p>
            <p v-else-if="movie.original_language == 'de'">
              Lingua originale: 🇩🇪
            </p>
            <p v-else>Lingua originale: {{ movie.original_language }}</p>
            <p>Voto: {{ movie.vote_average }}</p>
          </div>
        </div>
      </li>
      <!-- LISTA SERIE -->
      <li v-for="series in tvSerires" :key="series.id">
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
            <p>Titolo originale: {{ series.original_name }}</p>
            <p v-if="series.original_language == 'it'">Lingua originale: 🇮🇹</p>
            <p v-else-if="series.original_language == 'fr'">
              Lingua originale: 🇫🇷
            </p>
            <p v-else-if="series.original_language == 'es'">
              Lingua originale: 🇪🇸
            </p>
            <p v-else-if="series.original_language == 'en'">
              Lingua originale: 🇬🇧
            </p>
            <p v-else-if="series.original_language == 'de'">
              Lingua originale: 🇩🇪
            </p>
            <p v-else>Lingua originale: {{ series.original_language }}</p>
            <p>Voto: {{ series.vote_average }}</p>
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
    gap: 10px;
    padding: 40px;

    li {
      width: calc((100% / 4) - 10px);
      min-height: 400px;
      border: 1px solid #555;
      cursor: pointer;
      transition: 200ms linear;

      &:hover {
        transform: scale(0.97);
      }

      .hover-info {
        height: 100%;
        padding: 10px;
        opacity: 0;
        background: rgba($color: #000000, $alpha: 0.3);
        transition: 200ms linear;
      }

      &:hover .hover-info {
        opacity: 1;
      }

      .title-wrapper {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
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
        padding-top: 5px;
      }
    }
  }
}
</style>
