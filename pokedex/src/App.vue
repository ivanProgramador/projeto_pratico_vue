<template>

  <div id="app">
    <div class="column  is-ffset-one-quarter" >
      <div v-for="(poke,index) in pokemons " :key="index" >
         <PokemonComponent :name="poke.name" :url="poke.url" :num="index + 1" />
     

   </div>

    </div>
   
   
  </div>
</template>






<script>
import axios from 'axios';
import PokemonComponent from './components/Pokemon-component.vue';

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
     
  },
  components:{
     PokemonComponent,
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
