<template>
    <div v-bind:style="{ 'background-image': 'url('+movie.backdrop_path+')' }" class="movie_detail">
        <div class="det">
            <h2>{{ movie.original_title }} details</h2>
            <div class="detail_top">
                <img :src="movie.poster_path" alt="">
                <div class="information">
                    <h3><span>Title:</span>{{ movie.original_title }}</h3>
                    <h3><span>Tagline:</span>{{ movie.tagline }}</h3>
                    <h3><span>Date:</span>{{ movie.release_date }}</h3>
                    <h3><span>Time:</span>{{ movie.runtime }} mins</h3>
                    <h3><span>Rating:</span>{{ movie.vote_average }}</h3>
                    <h3><span>Budget:</span>{{ movie.budget }}</h3>
                    <h3><span>Revenue:</span>{{ movie.revenue }}</h3>
                    <h3><span>Status:</span>{{ movie.status }}</h3>
                </div>
            </div>
            <div class="overview">
                <p class="head">Overview</p>
                <p class="para">{{ movie.overview }}</p>
            </div>
        </div>
    </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from '@/env'

export default {
    setup() {
        const movie = ref({});
        const route = useRoute();
        const options = {
                method: 'GET',
                headers: {
                    'X-RapidAPI-Key': env.apiKey,
                    'X-RapidAPI-Host': 'advanced-movie-search.p.rapidapi.com'
                }
            };

        onBeforeMount(() => {
            fetch(`https://advanced-movie-search.p.rapidapi.com/movies/getdetails?movie_id=${route.params.id}`, options)
                .then(response => response.json())
                .then(data => {
                    movie.value = data;
                    console.log(movie.value)
                })
        })
        return {
            movie
        }
    }
}

</script>

<style>
    /* * {
        outline: red solid 1px;
    } */

    .movie_detail {
        min-height:100vh;
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        position: relative;
    }

    .detail_top {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
    }
    @media screen and (max-width: 500px) {
        .detail_top {
            flex-direction: column;
            padding: 20px;
        }
    }
    .det {
        width: 100%;
        min-height: 100vh;
        background-color: rgba(0, 0, 0, 0.8);
    }
    .det h2 {
        font-size: 25px;
        text-align: center;
        padding: 20px;
        color: #ececec;
    }
    .detail_top img {
        width: 200px;
        border-radius: 10px;
        margin: 10px;

    }
    .information h3 {
        font-size: 18px;
    }
    .information h3 span {
        color: #cacaca;
        text-transform: lowercase;
        padding-right: 25px;
    }
    .overview {
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        flex-direction: column;
        margin: 15px;

    }
    .head {
        font-weight: 700;
        margin-top: 20px;
        margin-bottom: 10px;
    }
    .overview p {
        max-width: 600px;
    }
    .para {
        padding-bottom: 20px;
    }
    

</style>