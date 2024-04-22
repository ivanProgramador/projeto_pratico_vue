<template>

  <div id="app">
   
  </div>
</template>






<script>
import axios from 'axios';

//toda vez que o servidor é iniciado um objeto impleicito camado created e gerado 
// por isso toda a lógica dde requisição ficara dentro dele

export default {
  name: 'App',
  data(){
     return {
       pokemons:[]
     }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res=>{

      console.log(res.data.results);
      this.pokemons = res.data.results;
      console.log(this.pokemons);
        
    })
     
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
