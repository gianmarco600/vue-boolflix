<template>
    <div class="container-sm text-center clearfix">
        <h1>Trova film & tv-shows</h1>
        <h2 class="title">inserisci il titolo</h2>
        <input v-model="inputQuery" placeholder="Es: 'matrix'" @keyup.prevent="inputCalls" type="text" name="movieTitle" id="movieTitle" >
        <!-- <div @click="clean">clean</div> -->
        <!-- <div :class="[(queryOutputTS.length == 0 && queryOutputM.length == 0 ? 'show' : 'hidden')]" class="lastSearch col-sm-12">
            <ul class="">
                <li v-for="(text ,i) in LastSrc" :key="i">{{text}}</li>
            </ul>
        </div> -->
        <h2 v-if='queryOutputM.length != 0' class="_label f_l">Movies</h2>
        <h2 v-if='queryOutputTS.length != 0' class="_label f_r">Tv Shows</h2>
        <div :class="(queryOutputTS.length == 0 && queryOutputM.length == 0 ? 'hidden' : 'show')"  class="clearfix porta_scaffali  row justify-content-around">
            
            <div :class="[(queryOutputTS.length == 0 ? 'col-sm-12' : 'col-sm-6'), (queryOutputM.length == 0 ? 'hidden' : 'show')]">
                
                <div  class="row scaffale justify-content-center align-items-start">
                    <MovieCard  :class="[queryOutputTS.length == 0 ? 'col-sm-3' : 'col-sm-6']" class="_card" v-for="risultatoM in queryOutputM" :key="risultatoM.id"  :risultatoM="risultatoM"/>
                </div>
            </div>
            <div :class="[(queryOutputM.length == 0 ? 'col-sm-12' : 'col-sm-6') ,( queryOutputTS.length == 0 ? 'hidden' : 'show')]">
                
                <div class="row scaffale _TS justify-content-center align-items-start" >
                    <TvShowsCard :class="[queryOutputM.length == 0 ? 'col-sm-3' : 'col-sm-6']" class="_card" v-for="risultatoTS in queryOutputTS" :key="risultatoTS.id" :risultatoTS="risultatoTS"/>
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
    
    methods:{
        inputCalls(){
           
            if(this.inputQuery != this.lastInputQuery && this.inputQuery.length != 0){
                this.LastSrc.push(this.inputQuery);
                console.log("input :" + this.inputQuery)
                this.APIcallM();
                this.APIcallTS();
                this.lastInputQuery = this.inputQuery;
                // console.log('m' + this.queryOutputM);
                // console.log('ts' + this.queryOutputTS);
                
            }
            if (this.inputQuery.length == 0){
                    console.log("input :" + this.inputQuery)
                    this.queryOutputM == [];
                    this.queryOutputTS == [];
                    console.log('svuoto');
                    console.log(this.queryOutputTS.length)      
                }
            
    
        },
        APIcallM(){
            

            axios
            .get(this.ricercaApiUrlM, {
                params: {
                    api_key : '37810146412a45c0824ff15ce4b214ba',
                    query : this.inputQuery,
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
            
            axios
            .get(this.ricercaApiUrlTS, {
                params: {
                    api_key : '37810146412a45c0824ff15ce4b214ba',
                    query : this.inputQuery,
                    language : this.lang
                }
            })   
            .then(res => {
                this.queryOutputTS = res.data.results;
                
            })
            .catch((error) => {
            console.log('Errore : ' + error);
            });
        },
        clean(){
            this.queryOutputM == [];
            this.queryOutputTS == [];
            console.log(this.queryOutputTS.length)     
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

.title{
    color: $netRed;
    text-transform: uppercase;
    font-weight: 600;
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
    background-color:rgb(22, 22, 22);
    min-height: 60vh;
    padding: 20px;
    display: flex;
    flex-wrap: wrap;
    border: 5px solid $netRed;
    box-sizing: content-box;
    margin: 30px 10px;
    box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;

}

._card{
    padding: 10px;
    
    height: calc(13vw * 16 / 9);
    // max-height: 500px;
    &:hover{
        box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
    }
}

._TS{
    border: 5px solid $tvYell;
}

._label{
    display: inline-block;
}
</style>