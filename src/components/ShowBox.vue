<template>
    <div class="container-md">
        <input v-model="inputQuery" :keyup="APIcall" type="text" name="movieTitle" id="movieTitle" >
        <div class="scaffale">
            <MovieCard v-for="(risultato, i) in queryOutput" :key="i" :risultato="risultato"/>
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
            lastInputQuery:''
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
                    language : 'it-IT'
                }
            })   
            .then(res => {
                this.queryOutput = res.data.results;
                
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

.scaffale{
    width: 100%;
    background-color:rgb(86,77,77);
    min-height: 60vh;
    padding: 20px;
    display: flex;
    flex-wrap: wrap;
}

</style>