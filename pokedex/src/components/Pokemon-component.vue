<template>

    

            <div class="card">
                <div class="card-image">
                    <figure >
                    <img
                        :src="currentImg"
                        alt="Placeholder image"
                    />
                    </figure>
                </div>
                <div class="card-content">
                    <div class="media">
                    <div class="media-center">
                        
                    </div>
                    <div class="media-content">
                        <p class="title is-4">{{ num }} {{ upper(name) }}</p>
                        <p class="subtitle is-6">{{ this.pokemon.type}}</p>
                    </div>
                    </div>

                    <div class="content">
                        <button class="button is-normal" @click="mudarSprite" >Mudar sprite</button>
                    
                    
                    
                </div>
                </div>
            </div>

   
  
</template>

<script>
import axios from 'axios';

export default {
    created:function(){
        axios.get(this.url).then(res=>{
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
            console.log(this.pokemon);
        })
    },
    data(){
        /*  mesmo que eu faça a requisição e os dados 
            sejam mostrados na tela 
            eles so serão reativos as propriadades form definidas dentro desta função 
            data porque quando eu reuisito na funçõ created ele traz e mostra porém para mudar 
            caso um desses dados atualize eu teria de requisitar denovo,
            já eu colocando eles dentro da funfção data ela detecta sozinha qualquer mudança que aconteça
            nos dado da url e atualiza o componente  


          
        */
        return{
            isFront:true,
            currentImg:'',
            pokemon:{
             type:'',
             front:'',
             back:''
            }
        }
    },
    props:{
        num: Number,
        name: String,
        url: String
    },
    methods:{
        upper: function(value){
          var newName = value[0].toUpperCase() + value.slice(1)
          return newName;
      },
       mudarSprite: function(){
          if(this.isFront){
             this.isFront = false;
             this.currentImg = this.pokemon.back;
             
          }else{
            this.isFront = true;
            this.currentImg = this.pokemon.front;

          }
       }
    }
}
</script>

<style>

</style>