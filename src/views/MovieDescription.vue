<template>
    <div class="movie-description">
        <h2>{{movie.Title}}</h2>
        <div class="movie-description__info">
            <div class="movie-description__poster-wrap">
                <img 
                    :src="movie.Poster" alt="poster"/>
            </div>
            <div class="movie-description__about">
                <p><span>Country: </span>{{movie.Country}}</p>
                <p><span>Year: </span>{{movie.Year}}</p>
                <p><span>Genre: </span>{{movie.Genre}}</p>
                <p><span>Released: </span>{{movie.Released}}</p>
                <p><span>Director: </span>{{movie.Director}}</p>
                <p><span>Rating IMDB: </span>{{movie.imdbRating}}</p>
                <p><span>Runtime: </span>{{movie.Runtime}}</p>
                <p><span>Actors: </span>{{movie.Actors + '...'}}</p>
            </div>
        </div>
        <p class="movie-description__plot">{{movie.Plot}}</p>
    </div>
</template>

<script>
import {ref, onBeforeMount} from 'vue';
import { useRoute } from 'vue-router';
import env from '@/views/env.js';

export default {
    setup() {
        const movie = ref({});
        const route = useRoute();
        onBeforeMount(() => {
            fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&i=${route.params.id}&plot=full`)
            .then(response => response.json())
            .then(data => {
                movie.value = data;
            });
        });
        return {
            movie
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/assets/__variables.scss';
@import '@/assets/__mixins.scss';

.movie-description {
    @include media ($md) {
        max-width: $md;
        margin: auto;
    }

    h2 {
        padding: 15px;
        color: $secondary-color;
        box-shadow: $box-shadow-color;
        font-size: 20px;
        text-align: center;

        @include media ($min-lg) {
            padding: 30px;
            font-size: 30px;
        }
    }

    &__info {
        padding: 15px;
        display: flex;
        flex-direction: row;

            @include media ($min-lg) {
                gap: 50px;
        }
    }

    &__poster-wrap {
        display: flex;
        justify-content: center;
        max-width: 200px;
        height: auto;

        img {
            width: 85%;

            @include media ($min-lg) {
                width: 100%;
        }
        }
    }

    &__about {
        color: $text-color;
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding: 0 10px;
        border-radius: 8px;
        gap: 8px;
        font-size: 14px;
        background-color: $desc-color;

        span {
            color: $secondary-color;
        }

            @include media ($min-lg) {
                font-size: 18px;
                gap: 14px;
        }
    }

    &__plot {
        color: $text-color;
        padding: 10px 20px;
        font-weight: 400;
        letter-spacing: 0.01em;
        line-height: 1.3;
        background-color: $desc-color;
        border-radius: 8px;

            @include media ($min-lg) {
                font-size: 23px;
        }
    }
}
</style>