<template>
    <div class="_box">
        <div class="risultato"> 
            <h3>Titolo: <span>{{risultato.name || risultato.title}}</span> </h3>
            
            <h4>titolo originale: <span>{{risultato.original_name || risultato.original_title}}</span> </h4>
            
            <div class="row hustify-content-start align-items-center"> <h4 class="col">lingua:</h4> <country-flag class="flag col" :country='getLang(risultato.original_language)' size='normal' :alt="risultato.original_language"/> 
            </div>
            
            <div class="row hustify-content-start align-items-center">
            <h5 class="col">rating:</h5>
            <div> </div>
            </div>

            <h5>overview: <span>{{risultato.overview.slice(0, 75) + '...'}}</span></h5>
            
            <img v-if="!posterCheck(risultato.poster_path)" class="copertina" :src="imgPATH + 'w500' + risultato.poster_path" :alt="risultato.name || risultato.title">
            <div v-else  class="copertina _bg row align-items-center"><h6>{{risultato.name || risultato.title}}</h6></div>
        </div>
    </div>
</template>

<script>
import CountryFlag from 'vue-country-flag';

export default {
    name:"Card",
    props:[
        'risultato',
        
        ],
    components: {
        CountryFlag
    },
    data(){
        return{
            queryOutput:'',
            imgPATH: 'https://image.tmdb.org/t/p/'
        }
    },
    methods:{
        getLang(sigla){
            
            let country = sigla.slice(0,2);
            if(country == 'en'){
                country = 'us';
            }
            console.log(country);
            return country
        },
        posterCheck(comp){
            
            if (comp == null ){
                return true
            }
            return false
        }
    }
}

</script>

<style lang="scss" scoped>
@import '@/style/commons.scss';
@import '@/style/vars.scss';

.risultato{
    background-color: rgba(31, 31, 31, 0.52);
    color: white;
    height: 100%;
    // text-align: center;
    // padding: 15px;
    position: relative;
    // z-index: 1;
    overflow: hidden;
    // margin: 15px;
    text-align: left;
    .flag{
        display: inline-block;
        padding: 0;
        margin-left: -195px;
    }
    h3{
        margin-top: 7px;
    }
    h4,h5{
        margin-top: 2px;
    }
    h4,h3,h5{
        font-weight: 700;
        color: $netRed;
        font-size: 15px;
        display: block;
        text-transform: capitalize;
    }
    &:hover .copertina{
        opacity: 0.2;
        // z-index: 0;
        
    }
    span{
        color: white;
        font-size: 14px;
        font-weight: 100;
    }
}

.copertina{
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
    
}

._bg{
    background: rgb(0,0,0);
    background: linear-gradient(33deg, rgba(0,0,0,1) 0%, rgba(229,9,20,1) 71%); 
    padding: 10px;
    h6{
        font-size: 20px;
        font-weight: 500;
    }
}
</style>