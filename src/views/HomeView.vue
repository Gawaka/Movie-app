<template>
  <div class="home">
    <div class="title-card">
      <router-link to="/movie/tt0110912">
      <!-- <img class="title-card__img" 
          src="../assets/pulp-poster.jpg" 
          alt="pulp-fiction"> -->
        <img class="title-card__img" 
          src="https://i.pinimg.com/564x/89/41/e7/8941e71464be8fe81ade92a86817338e.jpg" 
          alt="pulp-fiction">
        <div class="title-card__description">
          <h3 class="title-card__name">Pulp fiction</h3>
          <p>
            The lives of two mob hitmen, a boxer, a gangster and his wife, and a pair of 
            diner bandits intertwine in four tales of violence and redemption.
          </p>
        </div>
      </router-link>
    </div>
    <form class="home__search" 
      @submit.prevent="searchMovies()">
      <input class="home__input" 
        type="text" 
        placeholder="Search Movie" 
        v-model="search">
      <button class="home__btn" 
        type="submit">
        SEARCH
      </button>
    </form>
    <div class="movies">
      <div class="movies__item" 
        v-for="movie in movies" 
        :key="movie.imdbID">
        <router-link class="movies__link" 
          :to="'/movie/' + movie.imdbID">
          <div class="movies__poster-wrap">
            <img class="movies__poster" 
              :src="movie.Poster" 
              alt="poster">
            <span class="movies__type">
              {{ movie.Type }}
            </span>
          </div>
          <div class="movies__description">
            <span class="movies__year">
              {{ movie.Year}}
            </span>
            <h3 class="movies__title">
              {{ movie.Title }}
              </h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/views/env.js';

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          movies.value = data.Search;
          search.value = "";
          console.log(movies.value);
        });
      }
    }

    return {
      search,
      movies,
      searchMovies
    }
  }
}
</script>

<style lang="scss">
@import '@/assets/__variables.scss';
@import '@/assets/__mixins.scss';

.title-card {
  padding-top: 15px;
  max-width: $min-lg;
  margin: auto;
  position: relative;

  &__img {
    display: block;
    width: 95%;
    height: 290px;
    margin: auto;
    object-fit: cover;
    position: relative;
    z-index: 0;
    box-shadow: $box-shadow-color;
    border: 2px solid $secondary-color;

      @include media ($min-lg) {
        width: 100%;
        height: 350px;
        border: 5px solid $secondary-color;
  }
  }

  &__description {
    width: 94%;
    margin: auto;
    padding: 15px;
    position: absolute;
    left: 0;
    right: 0;
    bottom: 2px;
    background-color: $desc-color;
    color: $text-color;
    font-weight: 400;
    letter-spacing: 0.02em;

      @include media ($min-lg) {
        width: 350px;
        left: 5px;
        bottom: 5px;
        margin: 0;
  }
  }

  &__name {
    margin-bottom: 15px;
    font-size: 20px;
  }
}

.home {
  min-width: $sm;
  margin: 0 auto;
  
  &__search {
    max-width: $min-lg;
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 15px;

    @include media ($min-lg) {
      flex-direction: row;
      gap: 15px;
      padding: 15px 0;
    }
  }

      &__input {
        outline: none;
        text-align: center;
        border: none;
        width: 300px;
        height: 53px;
        color: $text-color;
        background-color: $input-color;
        font-size: 20px;
        padding:  10px 15px;
        border-radius: 10px;
        margin-bottom: 15px;
        transition: 0.5s;

        @include media ($min-lg) {
          margin-bottom: 0;
          height: 53px;
          width: 900px;
        }

      &::placeholder {
        color: $text-color;
        opacity: 0.1;
      }

      &:focus {
        box-shadow: $box-shadow-color;
      }
    }

    &__btn {
      cursor: pointer;
      width: 100%;
      max-width: 300px;
      background-color: $secondary-color;
      padding: 15px;
      border-radius: 10px;
      color: $text-color;
      font-size: 20px;
      transition: 0.4s;
      border: none;

      &:active {
        background-color: $hover-color;
        box-shadow: $box-shadow-color;
      }

      &:hover {
        background-color: $hover-color;
        box-shadow: $box-shadow-color;
      }
    }
}

.movies {
  max-width: $min-lg;
  display: flex;
  flex-wrap: wrap;
  margin: auto;

  &__item {
    min-width: 50%;
    flex: 1 1 50%;
    padding: 15px 8px;
    transition: 0.5s ease-in-out;

    &:last-child {
      width: 30%;
      flex: 0 0 33%;
      padding-bottom: 50px;
    }

    &:hover {
      transform: scale(1.03);
    }

    @include media ($min-lg) {
      min-width: 30%;
      flex: 2 4 30%;
    }
  }

  &__link {
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  &__poster-wrap {
    position: relative;
    display: block;
  }

  &__poster {
    display: block;
    width: 100%;
    height: 300px;
    object-fit: cover;

    @include media ($md) {
      height: 485px;
    }
  }

  &__type {
    position: absolute;
    padding: 8px 15px;
    background-color: $secondary-color;
    color: $text-color;
    bottom: 20px;
    left: 0;
    text-transform: capitalize;
  }

  &__description {
    background-color: $min-color;
    padding: 15px 8px;
    flex: 1 1 100%;
    border-radius: 0 0 10px 10px;
  }

  &__year {
    color: $secondary-color;
    font-size: 13px;
    margin-bottom: 7px;
  }

  &__title {
    color: $text-color;
    font-weight: 600;
    font-size: 17px;
  }
}
</style>