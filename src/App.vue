<template>
 <div class="header">
  <h1 class="logo">Anime<span>hub</span></h1>
</div>
  <div class="field">
<div class="inputField">
  <!-- <searchIcon class="search"/> -->
<input type="text"  placeholder="search anime" v-model="input" class="input">
<label  class="lb">
  {{input}}
</label>
</div> 
<div class="info-search">
<h1>What are you looking for?</h1>
<h3>Find news of your favourite anime from over 10,000 anime</h3>
</div>
<div  v-for="response in responses" v-bind:key="response.id" class="countryCard">
  <div class="bgImage">
  <img :src="response.image_url || image " class="bgImage bg-bgImage">
  </div>
  <div class="info" > 
    <h1>{{response.title}}</h1>
    <p>{{response.synopsis}}</p>
    </div>
</div>
</div>
</template>

<script>
// import searchIcon from '../assets/search.svg'
import axios from 'axios'
export default {
     name:'App',
    //  components: {
    //    searchIcon,
    //  },
     data() {
       return {
          responses: [],
          input: '',
          image: require('../assets/_.jpeg')
       }
     },


     mounted() {

let params =  {q: this.query}
  const url = new URL("https://jikan1.p.rapidapi.com/search/anime");
  const headers = {"x-rapidapi-host": "jikan1.p.rapidapi.com",
                      "x-rapidapi-key": "b4f0d08510msh85920546c521edfp1a9d4fjsna24afb100d1e"};    
  url.search = new URLSearchParams(params)  

axios
  .get( url, {

  "method": "GET",
  "headers": headers,
  
})

.then((res) => {
    this.responses = res.data.results;
    console.log(this.responses);
})


.catch(err => {
	console.error(err);
});
 

     },



}
</script>

<style>
@import '../style/app.css'
</style>