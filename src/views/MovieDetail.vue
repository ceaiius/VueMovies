<template>
  <div class="movie-template">
      <h2>{{movie.Title}}</h2>
      <p>{{movie.Year}}</p>
      <img :src="movie.Poster" alt="Poster" class="featured-img">
      <p class="plot">{{movie.Plot}}</p>
  </div>
</template>

<script>
import {ref, onBeforeMount} from "vue"
import { useRoute } from 'vue-router';
import env from "@/env.js"
export default {
    setup(){
        const movie = ref({});
        const route = useRoute();

        onBeforeMount(()=>{
            fetch(`https://www.omdbapi.com?apikey=${env.apikey}&i=${route.params.id}&plot-full`)
            .then(res=>res.json())
            .then(data=>{
                movie.value = data;
            })
        });
        return{
            movie
        }
    }
}
</script>

<style lang="scss">
    .movie-template{
        padding: 16px;
        display: flex;
        flex-direction: column;
        
        h2{
            color: #FFF;
            font-size: 28px;
            font-weight: 600;
            margin-bottom: 16px;
            align-self: center;
        }
        .featured-img{
            display: block;
            max-width: 200px;
            margin: 16px;
            align-self: center;
        }
        p{
            color:#FFF;
            font-size: 18px;
            line-height: 1.4;
            align-self: center;
        }

        .plot{
            padding-top: 5%;
        }
    }
</style>