<template>
<div id="pokemon">
    
    <div class="card">
  <div class="card-image">
    <figure>
      <img :src="pokemon.front" alt="Placehouder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">

      <div class="media-content">
        <p class="title is-4">{{num}} - {{upper(name)}}</p>
        <p class="subtitle is-6">{{pokemon.type}}</p>
      </div>
    </div>

    <div class="content">
        <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar sprite</button>
      
    </div>
  </div>
</div>
</div>
</template>

<script>
import axios from 'axios'


export default {

    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.currentImg = this.pokemon.front
            
            console.log(this.pokemon)
        })
    },
    data(){
        return{
            pokemon: {
                isfront: true,
                currentImg: "",
                type: "",
                front: "",
                back: ""
            }
        }
    },
    props:{
        num: Number,
        name: String,
        url: String
    },
    methods: {
        
        upper: function(value){
            var newName = value[0].toUpperCase() + value.slice(1)
            return newName

        },
        mudarsprite: function(){
            if(this.isfront){
                this.isfront = false
                this.currentImg = this.pokemon.back
            }else{
                this.isfront = true
                this.currentImg = this.pokemon.front
            }
        }

        
    }
       
    
}
</script>

<style scoped>
    #pokemon{
        margin-top: 2px;
        background-color:crimson;
    }
</style>