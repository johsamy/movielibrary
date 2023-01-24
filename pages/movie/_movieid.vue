<template>
    <LoadingAnimation v-if="$fetchState.pending" />
    <div v-else class="container singleMovie d-flex align-center">
        <v-col>
            <v-img
            max-width="525"
            class="rounded-xl"
            :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
            ></v-img>
        </v-col>
        <v-col>
            <v-card-title>
                {{ movie.title }}
            </v-card-title>

            <v-card-text>
            <v-row
                align="center"
                class="mx-0"
            >
                <v-rating
                :value="4.5"
                length="8"
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
                Date de sortie :
                {{
                    new Date(movie.release_date).toLocaleString('fr-FR', {
                        month: "long",
                        day: "numeric",
                        year: "numeric"
                    })
                }}
            </div>

            <div class="my-4 text-subtitle-1">
                Durée : {{ movie.runtime }} minutes
            </div>

            <div class="my-4 text-subtitle-1">
                Synopsis : {{ movie.overview }}
            </div>
            </v-card-text>
        </v-col>
    </div>
</template>

<script>
import axios from "axios"

export default {
    name: "singleMovie",
    head() {
        return {
            title: this.movie.title,
        }
    },
    data() {
        return {
            movie: null
        }
    },
    async fetch() {
        await this.getSingleMovie();
    },
    fetchDelay: 1000,
    methods: {
        async getSingleMovie() {
            const data = axios.get(
                `https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=ca9cca9965b491a858c3b5736d140464&language=fr-FR`
            );
            const result = await data;
            this.movie = result.data;
            console.log(this.movie.genre_ids)
            console.log("test")
        }
    }
}
</script>
