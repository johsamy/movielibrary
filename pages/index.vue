<template>
  <div class="home">
    <!-- Search -->
    <v-row class="searchBar d-flex justify-center">
        <!-- Search params -->
        <v-col
          cols="6"
          sm="2"
          md="3"
        >
            <v-text-field label="Recherche" @keyup.enter="launchMovies(false)" outlined type="text" color="#90cea1" v-model.lazy="searchInput"></v-text-field>
        </v-col>
        <v-col
          cols="4"
          sm="1"
          md="1"
        >
            <v-select
            :items="years"
            label="Année"
            outlined
            color="#90cea1"
            v-model.lazy="searchYear"
            ></v-select>
        </v-col>
        <!-- Actions buttons depending of searched value -->
        <v-btn @click="launchMovies(false)" v-show="searchInput !== ''" color="#90cea1" class="ml-2 my-5 black--text">
            <v-icon dark>
                mdi-magnify
            </v-icon>
        </v-btn>
        <v-btn @click="launchMovies(true)" v-show="searchInput !== ''" color="#90cea1" class="ml-2 my-5 black--text">
            <v-icon dark>
                mdi-close
            </v-icon>
        </v-btn>
    </v-row>

    <!-- Loading -->
    <LoadingAnimation v-if="$fetchState.pending" />

    <!-- Movies -->
    <div v-else>
        <!-- Movies list -->
        <!-- Display list only is movies array is not empty -->
        <div v-if="movies.length || searchInput === ''" class="d-flex justify-space-around flex-wrap">
            <div v-for="(movie, index) in movies" :key="index" >
                <v-card
                    class="mx-auto my-12 d-flex justify-space-around flex-wrap"
                    max-width="300"
                    min-height="650"
                >
                    <v-img v-if="movie.poster_path"
                    height="350"
                    :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
                    ></v-img>
                    <v-img v-else
                    class="ml-8"
                    max-height="350"
                    :src="require(`~/assets/images/video.svg`)"
                    ></v-img>

                    <v-card-title
                    heigth="400">
                        {{ movie.title.slice(0,27) }}
                        <span v-if="movie.title.length > 27">...</span>
                    </v-card-title>

                    <v-card-text>
                        <v-row
                            align="center"
                            class="mx-0"
                        >
                            <v-rating
                            :value="movie.vote_average"
                            length="10"
                            color="amber"
                            dense
                            half-increments
                            readonly
                            size="14"
                            ></v-rating>

                            <div class="grey--text ms-4">
                                {{ movie.vote_average }}
                            </div>
                        </v-row>

                        <div class="my-4 text-subtitle-1">
                            Sortie :
                            {{
                                new Date(movie.release_date).toLocaleString('fr-FR', {
                                    month: "long",
                                    day: "numeric",
                                    year: "numeric"
                                })
                            }}
                        </div>
                        </v-card-text>

                        <v-divider class="mx-3"></v-divider>

                        <v-card-text>
                        <v-chip-group column>
                            <v-chip v-for="(id) in movie.genre_ids" :key="id" small>
                                {{ genres[id] }}
                            </v-chip>
                        </v-chip-group>
                    </v-card-text>

                    <v-card-actions>
                    <v-btn
                        color="deep-purple lighten-2"
                        text
                    >
                        <NuxtLink
                        class="button button-light"
                        :to="{ name: 'movies-movieid', params: { movieid : movie.id } }">
                            <ButtonIcon>plus</ButtonIcon>
                        </NuxtLink>
                    </v-btn>
                    </v-card-actions>
                </v-card>
            </div>
        </div>
        <div v-else>
            <ErrorAlert>
                Aucun résultat trouvé.
            </ErrorAlert>
        </div>
        <!-- Pagination -->
        <v-pagination
            v-model="page"
            :length="total_pages"
            :total-visible="10"
            @input="$fetch"
            color="#90cea1">
        </v-pagination>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
    head() {
        return {
            title: "Catalogue",
        }
    },
    data() {
        return {
            movies: [],
            searchedMovies: [],
            searchInput: '',
            searchYear: '',
            genres: [],
            page: 1,
            total_pages: 0
        }
    },
    async fetch() {
        if (this.searchInput === "") {
            await this.getMovies();
            return;
        }
        await this.getSearchMovies();
    },
    // Having time to show the loading animation
    fetchDelay: 1000,
    methods: {
        async getMovies() {
            this.movies = [];
            const data = axios.get(
                `https://api.themoviedb.org/3/movie/now_playing?api_key=ca9cca9965b491a858c3b5736d140464&language=fr-FR&page=${this.page}`
            );
            const result = await data;
            result.data.results.forEach((movie) => {
                this.movies.push(movie);
            });
            this.total_pages = result.data.total_pages;
        },
        async getSearchMovies() {
            this.movies = [];
            const data = axios.get(
                `https://api.themoviedb.org/3/search/movie?api_key=ca9cca9965b491a858c3b5736d140464&language=fr-FR&page=${this.page}&query=${this.searchInput}&year=${this.searchYear}`
            );
            const result = await data;
            result.data.results.forEach((movie) => {
                this.movies.push(movie);
            });
            this.total_pages = result.data.total_pages;
        },
        async getGenres() {
            this.genres = [];
            const data = axios.get(
                `https://api.themoviedb.org/3/genre/movie/list?api_key=ca9cca9965b491a858c3b5736d140464&language=fr-FR`
            );
            const result = await data;
            result.data.genres.forEach((genre) => {
                this.genres[genre.id] = genre.name;
            });
        },
        launchMovies(isSearched) {
            if (isSearched) {
                this.searchInput = "";
            }
            this.page = 1;
            this.$fetch();
        }
    },
    computed : {
        years () {
            const year = new Date().getFullYear()+4
            return Array.from({length: year - 1900}, (value, index) => 1901 + index)
        }
    },
    mounted () {
        this.getMovies();
    },
    created () {
        this.getGenres();
    }
}
</script>
