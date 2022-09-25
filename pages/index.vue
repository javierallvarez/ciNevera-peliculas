<template>
  <div class="home">
    <!-- Hero -->
    <Hero />

    <!-- Search -->
    <!-- <div class="container search">
      <input
        type="text"
        placeholder="Search"
        @keyup.enter="$fetch"
        v-model.lazy="searchInput"
      />
      <button v-show="searchInput !== ''" @click="clearSearch" class="button">
        Clear Search
      </button>
    </div> -->

    <!-- Loading Animation
    <Loading v-if="$fetchState.pending" /> -->

    <div class="container movies">
      <div id="movie-flex" class="movies-flex">
        <div class="movie" v-for="(movie, index) in movies" :key="index">
          <div class="movie-info">
            <img
              :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
              alt=""
            />
            <p class="review">{{ movie.vote_average }}</p>
            <p class="overview">{{ movie.overview }}</p>
          </div>

          <div class="info">
            <!-- Si titulo > 25 caracteres muestra '...' -->
            <p class="title">
              {{ movie.title.slice(0, 25)
              }}<span v-if="movie.title.length > 25">...</span>
            </p>

            <!-- Muestra la fecha en español -->
            <p class="release">
              Estreno:
              {{
                new Date(movie.release_date).toLocaleString("es-ES", {
                  month: "long",
                  day: "numeric",
                  year: "numeric",
                })
              }}
            </p>

            <!-- nuxt/router.js nos muestra un path name movies-movieid y path: "/movies/:movieid?", lo usamos en el siguiente link: -->
            <NuxtLink
              class="button button-light"
              :to="{ name: 'movies-movieid', params: { movieid: movie.id } }"
            >
              Más Info
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "home",
  head() {
    return {
      title: "Movie App - Latest Streaming Movie Info",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Get all the latest streaming movies in theaters & online",
        },
        {
          hid: "keywords",
          name: "keywords",
          content: "movies, stream, stremaing",
        },
      ],
    };
  },

  data() {
    return {
      movies: [],
      searchedMovies: [],
      searchInput: "",
    };
  },

  async fetch() {
    if (this.searchInput === "") {
      await this.getMovies();
      return;
    }

    if (this.searchInput !== "") {
      await this.searchMovies();
    }
  },
  fetchDelay: 1000,

  methods: {
    async getMovies() {
      const apiKey = "";
      const data = axios.get(
        `https://api.themoviedb.org/3/discover/movie?api_key=${apiKey}&year=2022&language=es-ES&page=1&sort_by=popularity.desc`
      );
      const result = await data;
      result.data.results.forEach((movie) => {
        this.movies.push(movie);
        console.log(this.movies);
      });
    },

    async searchMovies() {
      const apiKey = "";
      const data = axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&language=es-US&page=1&query=${this.searchInput}`
      );
      const result = await data;
      result.data.results.forEach((movie) => {
        this.searchedMovies.push(movie);
      });
    },
  },
};
</script>

<style lang="scss">
$princepal: #54f6c6;
$princepal-dark: #3ec49c;
$secondary: #ffcbcb;

.home {
  .loading {
    padding-top: 120px;
    align-items: flex-start;
  }

  .search {
    display: flex;
    padding: 32px 16px;

    input {
      max-width: 350px;
      width: 100%;
      padding: 12px 6px;
      font-size: 14px;
      border: none;

      &:focus {
        outline: none;
      }
    }

    .button {
      border-top-left-radius: 0;
      border-bottom-left-radius: 0;
    }
  }

  .movies {
    padding: 32px 16px;

    .movies-flex {
      display: flex;
      flex-wrap: wrap;
      gap: 2rem;
      justify-content: center;

      .movie {
        position: relative;
        display: flex;
        flex-direction: column;

        .movie-info {
          position: relative;
          overflow: hidden;

          &:hover {
            .overview {
              transform: translateY(0);
            }
          }

          img {
            display: block;
            width: 120px;
            height: 100%;

            @media (min-width: 500px) {
              width: 300px;
              height: 100%;
            }
          }

          .review {
            position: absolute;
            top: 0;
            left: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 40px;
            height: 40px;
            background-color: $princepal-dark;
            color: #fff;
            border-radius: 0 0 16px 0;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
              0 2px 4px -1px rgba(0, 0, 0, 0.06);
          }

          .overview {
            line-height: 1.5;
            position: absolute;
            bottom: 0;
            background: linear-gradient(to bottom, $princepal 0%, black 80%);
            padding: 12px;
            color: #fff;
            transform: translateY(100%);
            transition: 0.3s ease-in-out all;
          }
        }

        .info {
          margin-top: auto;
          @media (max-width: 500px) {
            display: none;
          }

          .title {
            margin-top: 8px;
            color: #fff;
            font-size: 20px;
            font-family: "Bodoni Moda";
            font-weight: 600;
            font-style: italic;
          }

          .release {
            margin-top: 8px;
            color: #c9c9c9;
          }

          .button {
            margin-top: 8px;
          }
        }
      }
    }
  }
}
</style>
