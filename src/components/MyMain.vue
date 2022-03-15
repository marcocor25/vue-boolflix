<template>
  <!-- MAIN CONTAINER -->
  <div class="container">
    <!-- LOGO -->
    <figure class="logo">
      <img src="../assets/img/Boolflix.svg" />
    </figure>
    <!-- INPUT -->
    <div class="input-wrapper">
      <input
        type="search"
        placeholder="Cerca film e serie tv..."
        @keyup.enter="cercaFilm(), cercaSerie()"
        v-model="search"
      />
      <button @click="cercaFilm(), cercaSerie()">Cerca</button>
    </div>
    <!-- CONTAINER LISTE -->
    <ul class="list-container">
      <!-- LISTA FILM -->
      <li v-for="movie in movies" :key="movie.id">
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
      </li>
      <!-- LISTA SERIE -->
      <li v-for="series in tvSerires" :key="series.id">
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
        })
        .catch((err) => {
          console.log(err.response);
        });

      this.search = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  width: 60vw;
  height: 100vh;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;

  .logo {
    width: 200px;
    filter: drop-shadow(3px 3px 1px black);
  }

  .input-wrapper {
    width: 500px;
    display: flex;
    gap: 5px;

    input {
      flex-grow: 1;
      height: 30px;
      padding: 0 5px;
      border-radius: 5px;
      border: 1px solid #555;
      color: currentColor;
      background: #222;

      &:focus-visible {
        outline: none;
      }
    }

    button {
      padding: 0 10px;
      border-radius: 5px;
      border: 1px solid #555;
      color: currentColor;
      background: #222;
    }
  }

  .list-container {
    width: 500px;
    padding-right: 10px;
    overflow: auto;
    display: flex;
    flex-direction: column;
    gap: 20px;

    li {
      flex-shrink: 0;
      min-height: 100px;
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #555;
      background: #222;

      .title-wrapper {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        border-bottom: 1px solid #d81f26;

        .badge {
          padding: 0 5px;
          font-size: 12px;
          border-radius: 5px;
          cursor: default;
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
