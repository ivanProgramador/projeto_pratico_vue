<template>

  <div id="app">
    <div class="column  is-ffset-one-quarter" >
      <hr>
      <h4 class="is-size-4">Pokedex</h4>

      <input type="text" placeholder="Busca pelo nome" v-model="busca" class="input is-rounded" >
      <button class="button is-normal is-success" id="buscaBtn" @click="buscar">Busca</button>




      <div v-for="(poke,index) in filteredPokemons " :key="poke.url" >
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
       pokemons:[],
       filteredPokemons:[],
       busca:''
     }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res=>{

      console.log(res.data.results);
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    
        
    })
     
  },
  components:{
     PokemonComponent,
  },
  methods:{

    buscar:function(){
       
        this.filteredPokemons = this.pokemons;
        if(this.busca == '' || this.busca == ' '){
            this.filteredPokemons = this.pokemons;
        }else{
             this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
        }
    }

  },
  computed:{
   /*  resultadoBusca: function(){
        if(this.busca == '' || this.busca == ' '){
            return this.pokemons;
        }else{
             return this.pokemons.filter(pokemon => pokemon.name == this.busca);
        }
     }
    */
     
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

#buscaBtn{
    margin-top: 2%;
}
</style>
