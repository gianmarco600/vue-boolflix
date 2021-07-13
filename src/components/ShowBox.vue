<template>
    <div class="container-sm text-center">
        <h1>Trova film & tv-shows</h1>
        <h2>inserisci il titolo</h2>
        <input v-model="inputQuery" placeholder="Es: 'matrix'" :keyup="APIcallM" type="text" name="movieTitle" id="movieTitle" >
        <div class="porta_scaffali row justify-content-around">
            <div class="col-sm-5 " :class="[(queryOutputTS.length == 0 ? 'col-sm-12' : 'col-sm-5'), (queryOutputM.length == 0 ? 'hidden' : 'show')]">
                <div  class="row scaffale justify-content-center align-items-start">
                    <MovieCard  :class="[queryOutputTS.length == 0 ? 'col-sm-3' : 'col-sm-10']" class="_card" v-for="risultatoM in queryOutputM" :key="risultatoM.id" :risultatoM="risultatoM"/>
                </div>
            </div>
            <div class="col-sm-5 " :class="[(queryOutputM.length == 0 ? 'col-sm-12' : 'col-sm-5') ,( queryOutputTS.length == 0 ? 'hidden' : 'show')]">
                <div class="row scaffale _TS justify-content-center align-items-start" >
                    <TvShowsCard :class="[queryOutputM.length == 0 ? 'col-sm-3' : 'col-sm-10']" class="_card" v-for="risultatoTS in queryOutputTS" :key="risultatoTS.id" :risultatoTS="risultatoTS"/>
                </div>
            </div>
        </div>
           <!-- :class="(queryOutputTS.length == 0 ? 'col-sm-12' : 'col-sm-6' , queryOutputM.length == 0 ? 'hidden' : 'show'   )"  
           :class="(queryOutputM.length == 0 ? 'hidden' : 'show')"
           :class="(queryOutputTS.length == 0 ? 'col-sm-12' : 'col-sm-6')"
           :class="( (queryOutputM.length == 0 ? 'col-sm-12' : 'col-sm-5'),( queryOutputTS.length == 0 ? 'hidden' :  'show'))"
           :class="(queryOutputM.length == 0 ? 'col-sm-3' : 'col-sm-6')" -->
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
    width: 100%;
    background-color:rgb(86,77,77);
    min-height: 60vh;
    padding: 20px;
    display: flex;
    flex-wrap: wrap;
    border: 10px solid $netRed;

}

._card{
    padding: 10px;
    
    height: 470px;
    // max-height: 500px;
}

._TS{
    border: 10px solid #ddb021;
}

</style>