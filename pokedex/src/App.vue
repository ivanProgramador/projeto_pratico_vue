<template>

  <div id="app">
    <div class="column  is-ffset-one-quarter" >
      <hr>
      <h4 class="is-size-4">Pokedex</h4>

      <input type="text" placeholder="Busca pelo nome" v-model="busca" class="input is-rounded" >

      <!-- 1 esse botão tem o evento click para acionar a função de busca-->
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
  
      // 2 - um array vazio foi criado para guardar os pokemnos filtrados 

      this.filteredPokemons = res.data.results;
    
        
    })
     
  },
  components:{
     PokemonComponent,
  },
  methods:{
   
    buscar:function(){
       //a função de busca chama o array vazio e coloca todos os pokemons dentro dele 
      
        this.filteredPokemons = this.pokemons;

        // depois testa o campo de busca pra ver se o susario digitou alguma coisa 

        if(this.busca == '' || this.busca == ' '){
          // se não digitou o array de pokemons filtrados recebe so os pokemnos que já estavam lá
          // e continua exibindo todos 

            this.filteredPokemons = this.pokemons;

        }else{
          // se o cliente tiver digitado alguma coisa no campo de busca 
          // ele pega o array de pokemons faz um filtro com base na propriadade nome 
          // e deixa somente o pokemon que o cliente buscou dentro array e exibe somente ele 

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
