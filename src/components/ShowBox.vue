<template>
    <div class="container-md text-center">
        <h1>Trova film</h1>
        <input v-model="inputQuery" placeholder="Es: 'matrix'" :keyup="APIcall" type="text" name="movieTitle" id="movieTitle" >
        <div class="scaffale">
            <MovieCard v-for="risultato in queryOutput" :key="risultato.id" :risultato="risultato"/>
        </div>
    </div>
</template>

<script>


import MovieCard from '@/components/MovieCard.vue';
import axios from 'axios';

export default {
    name:'ShowBox',
    components:{
        MovieCard
    },
    data(){
        return{
            ricercaApiUrl: 'https://api.themoviedb.org/3/search/movie?',
            inputQuery:'',
            queryOutput:[],
            LastSrc:[],
            lastInputQuery:'',
            lang:'it-IT'
        }
    },
updated() {
        
    if (this.inputQuery!= '' && this.inputQuery!=this.lastInputQuery){
        this.APIcall();
        this.lastInputQuery = this.inputQuery;
        console.log(this.queryOutput);
        console.log(this.queryOutput.length)
    }
        
},
    
    methods:{
        APIcall(){
            let inputText = this.inputQuery;
            this.LastSrc.push(this.inputQuery);

            axios
            .get(this.ricercaApiUrl, {
                params: {
                    api_key : '37810146412a45c0824ff15ce4b214ba',
                    query : inputText,
                    language : this.lang
                }
            })   
            .then(res => {
                this.queryOutput = res.data.results;
                
            })
            .catch((error) => {
            console.log('Errore : ' + error);
        });
        },
        // changeLang(){
        //     this.lang ==
        // }
    }

}
</script>

<style lang="scss" scoped>
@import '@/style/commons.scss';
@import '@/style/vars.scss';

h1{
    margin: 40px;
    color: black;
    background-color: $netRed;
    border-radius: 15px;
}

input{
    margin: 20px;
    background-color: $netRed;
    color: black;
    padding: 7px;
    height: 40px;
    width: 300px;
    border: none;
    font-size: 25px;
    font-weight: 500;
    border-radius: 15px;
}

.scaffale{
    width: 100%;
    background-color:rgb(86,77,77);
    min-height: 60vh;
    padding: 20px;
    display: flex;
    flex-wrap: wrap;
}

</style>