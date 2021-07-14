<template>
  <div id="app">
    <Header class="_header" @input='passInput'/>
    <ShowBox class="_main" :queryOutputM='queryOutputM' :queryOutputTS='queryOutputTS'/>
  </div>
</template>

<script>
import ShowBox from './components/ShowBox.vue';
import Header from './components/Header.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    ShowBox,
    Header
  },
  data(){
    return{
      inputQuery:'',
      ricercaApiUrlM: 'https://api.themoviedb.org/3/search/movie?',
      ricercaApiUrlTS: 'https://api.themoviedb.org/3/search/tv?',
      // inputQuery:'',
      queryOutputM:[],
      queryOutputTS:[],
      LastSrc:[],
      lastInputQuery:'',
      lang:'it-IT',
      trendingURL:'https://api.themoviedb.org/3/trending/'
      
    }
  },
  mounted(){
        this.trendingRender();
        console.log(this.queryOutputTS);
        console.log(this.queryOutputM);
  },
  methods:{
    passInput(input){
      this.inputQuery = input;
      this.inputCalls()
    },
    inputCalls(){
            if (this.inputQuery.length == 0){
                this.trendingRender();           ;      
            }
            if(this.inputQuery != this.lastInputQuery && this.inputQuery.length != 0){
                this.LastSrc.push(this.inputQuery);
                console.log("input :" + this.inputQuery)
                this.APIcallM();
                this.APIcallTS();
                this.lastInputQuery = this.inputQuery;
                // console.log('m' + this.queryOutputM);
                // console.log('ts' + this.queryOutputTS);
                
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
        trendingRender(){
            let urlM = this.trendingURL + 'movie/day';
            let urlTS = this.trendingURL + 'tv/day';
            axios
                .get(urlM, {
                    params: {
                        api_key : '37810146412a45c0824ff15ce4b214ba',
                    }
                })   
                .then(res => {
                    this.queryOutputM = res.data.results;
                    
                })
                .catch((error) => {
                console.log('Errore : ' + error);
                });
                // let url = this.trendingURL + 'movie/day';

            axios
                .get(urlTS, {
                    params: {
                        api_key : '37810146412a45c0824ff15ce4b214ba',
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

<style lang="scss">
@import '@/style/commons.scss';
@import '@/style/vars.scss';

p{
  color: white;
}

._header{
  position: fixed;
  top: 0;
  z-index: 999;
}


</style>
