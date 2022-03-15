<template>
  <div class="container">
    <figure class="logo">
      <img src="../assets/img/Boolflix.svg" />
    </figure>
    <div class="input-wrapper">
      <input
        type="search"
        placeholder="Cerca film e serie tv..."
        @keyup.enter="cercaFilm"
        v-model="search"
      />
      <button @click="cercaFilm()">Cerca</button>
    </div>
    <ul class="film-container">
      <li v-for="movie in movies" :key="movie.id">
        <h3>Titolo: {{ movie.title }}</h3>
        <p class="original-title">
          Titolo originale: {{ movie.original_title }}
        </p>
        <p v-if="movie.original_language == 'it'" class="lang">Lingua: 🇮🇹</p>
        <p v-else-if="movie.original_language == 'fr'" class="lang">
          Lingua: 🇫🇷
        </p>
        <p v-else-if="movie.original_language == 'es'" class="lang">
          Lingua: 🇪🇸
        </p>
        <p v-else-if="movie.original_language == 'en'" class="lang">
          Lingua: 🇬🇧
        </p>
        <p v-else class="lang">Lingua: {{ movie.original_language }}</p>
        <p class="vote">Voto: {{ movie.vote_average }}</p>
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

  .film-container {
    width: 500px;
    padding-right: 10px;
    overflow: auto;
    display: flex;
    flex-direction: column;
    gap: 20px;

    li {
      flex-shrink: 0;
      height: 100px;
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #555;
      background: #222;
    }
  }
}
</style>
