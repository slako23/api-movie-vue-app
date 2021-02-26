<template>
  <div class="home">
    <h3 class="what-would">What Would You Like To Watch?</h3>
    <div class="feature-card">
      <router-link to="/movie/tt0259484">
        <img src="https://m.media-amazon.com/images/M/MV5BZWU5YmRhODYtM2Y2Ny00NTUzLWEwZGUtYzYyMjQwZmIwYTgxXkEyXkFqcGdeQXVyMTczNjQwOTY@._V1_SX300.jpg" alt="Paid In Full Poster" class="featured-img" />
        <div class="detail">
          <h3>Paid In Full</h3>
          <p>
            A teen, envious of the high-rolling lifestyle of his drug-dealing friends, joins the business and moves to the top of the Harlem drug world while rivals conspire to bring about his fall.
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search" />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
     <div class="movie" v-for="movie in movies" :key="movie.imdbID">
       <router-link v-bind:to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster">
            <div class="type">
              {{ movie.Type }}
            </div>
          </div>
          <div class="detail">
              <p class="year">{{ movie.Year }}</p>
              <h3>{{ movie.Title }}</h3>
            </div>
       </router-link>
     </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from 'vue';
import env from '@/env.js';


export default {
    setup(){
      const search = ref("");
      const movies = ref([]);

      const SearchMovies = () => {
        if(search.value != "") {
          fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then ( response => response.json())
          .then( data => {
            movies.value = data.Search;
            search.value = ""
;          });
        }
      }

      return{
        search,
        movies,
        SearchMovies
      }
    }
}
</script>


<style lang="scss">
@media only screen and (min-device-width: 360px) and (max-device-width: 768px) and (orientation:portrait) {
    .featured-img{
      display: block;
      width:100%;
      position: relative;
    }
}

   .home {
      .feature-card {
        position: relative;
        
        .featured-img {
          display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;
          height: 700px;
          object-fit: cover;
          position: relative;
          z-index: 0;
        }
        .detail {
          position: absolute;
          left: 0;
          right: 0;
          bottom: 0;
          background-color: rgba(0, 0, 0, 0.6);
          padding: 16px;
          z-index: 1;
          h3 {
            color:#FFF;
            margin-bottom: 16px;
          }
          p {
            color: #FFF;
          }
        }
      }
      .search-box {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 16px;
        input {
          display: block;
          appearance: none;
          border: none;
          outline: none;
          background: none;
          &[type="text"] {
            width: 100%;
            color: #000;
            background-color: #FFF;
            font-size: 20px;
            padding: 10px 16px;
            border-radius: 8px;
            margin-bottom: 15px;
            transition: 0.4s;
            &::placeholder {
              color: #000;
            }
            &:focus {
              box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
            }
          }
          &[type="submit"] {
            width: 100%;
            max-width: 300px;
            background-color: #FF0000;
            padding: 16px;
            border-radius: 8px;
            color: #FFF;
            font-size: 20px;
            text-transform: uppercase;
            transition: 0.4s;
            &:active {
              background-color: #3B8070;
            }
          }
        }
      }
      .movies-list {
        display: flex;
        flex-wrap: wrap;
        margin: 0px 8px;
        .movie {
          max-width: 50%;
          flex: 1 1 50%;
          padding: 16px 8px;
          .movie-link {
            display: flex;
            flex-direction: column;
            height: 100%;
            .product-image {
              position: relative;
              display: block;
              img {
                display: block;
                width: 100%;
                height: 275px;
                object-fit: cover;
              }
              .type {
                position: absolute;
                padding: 8px 16px;
                background-color: #FF0000;
                color: #FFF;
                bottom: 16px;
                left: 0px;
                text-transform: capitalize;
              }
            }
            .detail {
              background-color: #FF0000;
              padding: 16px 8px;
              flex: 1 1 100%;
              border-radius: 0px 0px 8px 8px;
              .year {
                color: #FFF;
                font-size: 14px;
              }
              h3 {
                color: #FFF;
                font-weight: 600;
                font-size: 18px;
              }
            }
          }
        }
      }
  
}

.what-would{
      display: block;
      text-align: center;
      margin:10px;
      color:#FFF;
      position: relative;
      }

</style>
