<template>
    <div class="container-md text-center">
        <h1>Trova film</h1>
        <input v-model="inputQuery" placeholder="Es: 'matrix'" :keyup="APIcallM" type="text" name="movieTitle" id="movieTitle" >
        <div class="porta_scaffali row justify-content-around">
            <div class="col-sm-5">
                <div class="row scaffale ">
                    <MovieCard class="_card col-sm-6" v-for="risultatoM in queryOutputM" :key="risultatoM.id" :risultatoM="risultatoM"/>
                </div>
            </div>
            <div class="col-sm-5">
                <div class="row scaffale _TS">
                    <TvShowsCard class="_card col-sm-6" v-for="risultatoTS in queryOutputTS" :key="risultatoTS.id" :risultatoTS="risultatoTS"/>
                </div>
            </div>
        </div>
            
    </div>
</template>

<script>


import MovieCard from '@/components/MovieCard.vue';
import axios from 'axios';
import TvShowsCard from '@/components/TvShowsCard.vue';

export default {
    name:'ShowBox',
    components:{
        MovieCard,
        TvShowsCard
    },
    data(){
        return{
            ricercaApiUrlM: 'https://api.themoviedb.org/3/search/movie?',
            ricercaApiUrlTS: 'https://api.themoviedb.org/3/search/tv?',
            inputQuery:'',
            queryOutputM:[],
            queryOutputTS:[],
            LastSrc:[],
            lastInputQuery:'',
            lang:'it-IT'
        }
    },
updated() {
        
    if (this.inputQuery!= '' && this.inputQuery!=this.lastInputQuery){
        this.APIcallM();
        this.APIcallTS();
        this.lastInputQuery = this.inputQuery;
        console.log('m' + this.queryOutputM);
        console.log('ts' + this.queryOutputTS);

    }
        
},
    
    methods:{
        APIcallM(){
            let inputText = this.inputQuery;
            this.LastSrc.push(this.inputQuery);

            axios
            .get(this.ricercaApiUrlM, {
                params: {
                    api_key : '37810146412a45c0824ff15ce4b214ba',
                    query : inputText,
                    language : this.lang
                }
            })   
            .then(res => {
                this.queryOutputM = res.data.results;
                
            })
            .catch((error) => {
            console.log('Errore : ' + error);
            });
        },
        APIcallTS(){
            let inputText = this.inputQuery;
            axios
            .get(this.ricercaApiUrlTS, {
                params: {
                    api_key : '37810146412a45c0824ff15ce4b214ba',
                    query : inputText,
                    language : this.lang
                }
            })   
            .then(res => {
                this.queryOutputTS = res.data.results;
                
            })
            .catch((error) => {
            console.log('Errore : ' + error);
            });
        }
        
        
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
    padding:15px;
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
    background-color:rgb(86,77,77);
    min-height: 60vh;
    padding: 20px;
    display: flex;
    flex-wrap: wrap;
    border: 10px solid $netRed;
}

._card{
    padding: 10px;
}

._TS{
    border: 10px solid #ddb021;
}

</style>