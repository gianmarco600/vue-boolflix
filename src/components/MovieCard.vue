<template>
  <div class="risultato film "> 
      <h3>Titolo:</h3>
      {{risultato.title}}
      <h4>titolo originale:</h4>
      {{risultato.original_title}}
      <h4>lingua:</h4>
      <country-flag :country='getLang(risultato.original_language)' :alt="risultato.original_language" size='normal'/> 
      <h5>rating:</h5>
      {{risultato.vote_average}}
  </div>
</template>

<script>

import CountryFlag from 'vue-country-flag';

export default {
    name:'MovieCard',
    props:[
        'risultato',
    ],
    components: {
        CountryFlag
    },
    data(){
        return{
            queryOutput:''
        }
    },
    methods:{
        getLang(film){
            
            let country = film.slice(0,2);
            if(country == 'en'){
                country = 'us';
            }
            console.log(country);
            return country
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/style/commons.scss';
@import '@/style/vars.scss';

.risultato{
    background-color: rgb(31, 31, 31);
    color: white;
    // text-align: center;
    padding: 15px;
    margin: 15px;
    h4,h5{
        margin-top: 10px;
    }
    h4,h3,h5{
        color: $netRed;
    }
}
.film{
    width: calc(100% / 4 - 30px);

}

</style>