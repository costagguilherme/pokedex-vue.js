<template>
    <div >
        <div class="card mb-6">
            <div class="card-image">
                <figure >
                    <img :src="currentImg" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{num}} - {{name | upper }}</p>
                        <p class="subtitle is-6">Type: {{pokemon.type}}</p>
                    </div>
                </div>

                <div class="content">
                    <button @click="changePosition()" class="button is-primary is-small is-fullwidth">Mudar visualização</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        
        created () {
            axios.get(this.url).then(res => {

                this.pokemon.type = res.data.types[0].type.name 
                this.pokemon.front = res.data.sprites.front_default 
                this.pokemon.back = res.data.sprites.back_default
                this.currentImg = this.pokemon.front
            }).catch(error => {console.log(error)})
        },

        data () {
            return {
                pokemon: {
                    type: "", 
                    front: "", // Imagem frontal
                    back: "" // Imagem traseira
                },

                isFront: true,
                currentImg: ''
            }
        },

        props: {
            num: Number,
            name: String,
            url: String
        },

        filters: {
            upper (value) {
                let newName = value[0].toUpperCase() + value.slice(1)
                return newName
            }
        },

        methods: {
            changePosition() {
                if (this.isFront) {
                    this.isFront = false
                    this.currentImg = this.pokemon.back
                } else {
                    this.isFront = true
                    this.currentImg = this.pokemon.front
                }
            }
        }
    }
</script>

<style>
   
</style>