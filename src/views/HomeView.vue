<template>
  <div class="home">
    <div class="featured_card">

      <header>
        <router-link to="/">
          <h1><span>Movie</span>Discovery</h1>
        </router-link>
      </header>
      <router-link to="/">
        <img src="@/images/wall.jpg" alt="app poster" class="featured_img">
        <div class="details">
          <p>Movie Discovery provides up-to-date information about new and upcoming films, including detailed descriptions, cast information, reviews, and trailers. With our easy-to-use search engine, you can quickly find information about any movie ever made. Plus, our site also offers exclusive content and news, so you can stay ahead of the curve when it comes to the latest films. Try Movie Discovery today and unlock the world of cinema!</p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies() " class="search_box">
      <input type="text" placeholder="eg. avengers" v-model="search">
      <input type="submit" value="search">
    </form>

    <div class="movies_list">

      <div class="movie" v-for="movie in movies" :key="movie.id">
        <router-link :to="'/movie/' + movie.id" class="movie_link">
          <img :src="movie.poster_path" alt="movie poster" class="product_img">
          <div class="detail">
            <div class="type"> {{ movie.vote_average }} </div>
            <h3>{{ movie.original_title }}</h3>
            <h4>{{ movie.release_date }}</h4>
          </div>
        </router-link>
      </div>

      <div class="movie" v-for="show in shows" :key="show.id">
        <router-link :to="'/movie/' + show.id" class="movie_link">
          <img :src="show.poster_path" alt="movie poster" class="product_img">
          <div class="detail">
            <div class="type"> {{ show.vote_average }} </div>
            <h3>{{ show.original_title }}</h3>
            <h4>{{ show.release_date }}</h4>
          </div>
        </router-link>
      </div>

    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import env from "@/env";

export default {
  setup() {
    const search =ref('');
    const movies = ref([]);
    const shows = ref([]);
    const options = {
      method: 'GET',
      headers: {
        'X-RapidAPI-Key': env.apiKey,
        'X-RapidAPI-Host': 'advanced-movie-search.p.rapidapi.com'
      }
    };
    const SearchMovies = () => {
      if (search.value != '') {
        fetch(`https://advanced-movie-search.p.rapidapi.com/search/movie?query=${search.value}&page=1`, options)
          .then(response => response.json())
          .then(data => {
            movies.value = data.results;
            search.value = '';
            shows.value = '';
            console.log(movies.value);
          });
      }
    }
    onBeforeMount(() => {
      if (search.value == '') {
        fetch(`https://advanced-movie-search.p.rapidapi.com/search/movie?query=avengers&page=1`, options)
        .then(response => response.json())
        .then(data => {
          shows.value = data.results;
          console.log(shows.value);
        });
      }
    })

    return {
      search,
      movies,
      shows,
      SearchMovies,
    }
  }
}
</script>

<style scoped>

  header {
    display: flex;
    position: absolute;
    top: 5;
    left: 0;
    align-items: center;
    justify-content: flex-start;
    padding: 10px 0;
    z-index: 10;
    margin-left: 16px;
  }
  
  header h1 {
    color: #ffffff;
    font-size: 28px;
    background: #000000;
    padding: 20px;
    border-radius: 15px;
  }
  
  header h1 span {
    letter-spacing: 5px;
  }
  

  .featured_card {
    position: relative;
  }
  .featured_img {
    display: block;
    width: 100%;
    height: 400px;
    object-fit: cover;
    position: relative;
    z-index: 0;
  }
  .details {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0));
    padding: 20px;
    z-index: 1;
    color: #ffffff;

  }
  .details p {
    max-width: 600px;
  }
  .search_box {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 16px;
  }
  .search_box input {
    display: flex;
    appearance: none;
    border: none;
    outline: none;
    background: none;

  }
  .search_box input[type='text'] {
    width: 90%;
    color: #000000;
    background: #ffffff;
    border: 2px solid rgba(255, 255, 255, 0);
    
    font-size: 20px;
    padding: 10px 16px;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
    transition: 0.4s;
  }
  input::placeholder {
    color: #3f3f3f;
  }

  input[type='text']:focus {
    background: #000000;
    color: #ffffff;
    border: 2px solid #ffffff;
  }
  .search_box input[type='submit'] {
    width: 100%;
    max-width: 100px;
    background: #ffffff;
    color: #000000;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    padding: 14px;
    font-size: 17px;
    text-transform: uppercase;
    transition: 0.4s;
  }
  .movies_list {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
  }
  .movie {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    position: relative;
  } 
  .movie_link {
    position: relative;
    height: 300px;
    width: 230px;
    margin: 15px;
  }
  .movie_link img {
    height: 300px;
    width: 230px;
    border-radius: 10px;
    object-fit: cover;
  }
  .detail {
    position: absolute;
    display: flex;
    flex-direction: column;
    padding: 10px;
    background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0));
    color: #fff;
    height: fit-content;
    bottom: 0;
    left: 0;
    right: 0;
  }
  .detail .type {
    padding: 15px;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #000;
    color: #fff;
  }



</style>
