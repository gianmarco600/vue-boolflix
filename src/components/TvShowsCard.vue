<template>
    <div class="_box">
        <div class="risultatoTS film "> 
            <h3>Titolo:</h3>
            {{risultatoTS.name}}
            <h4>titolo originale:</h4>
            {{risultatoTS.original_name}}
            <h4>lingua:</h4>
            <country-flag :country='risultatoTS.original_language' size='normal'/> 
            <h5>rating:</h5>
            {{risultatoTS.vote_average}}
            <h5>overview</h5>
            {{risultatoTS.overview.slice(0, 75) + '...'}}
            <img v-if="!posterCheck(risultatoTS.poster_path)" class="copertina" :src="imgPATH + 'w500' + risultatoTS.poster_path" :alt="risultatoTS.name">
            <div v-else  class="copertina _bg row align-items-center"><h6>{{risultatoTS.name}}</h6></div>
        </div>
    </div>
</template>

<script>
import CountryFlag from 'vue-country-flag';

export default {
    name:"TvShowsCard",
    props:[
        'risultatoTS',
        
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
        getLang(tvShow){
            
            let country = tvShow.slice(0,2);
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

.risultatoTS{
    background-color: rgba(31, 31, 31, 0.52);
    color: white;
    height: 100%;
    // text-align: center;
    padding: 15px;
    position: relative;
    z-index: 1;
    overflow: hidden;
    // margin: 15px;
    h4,h5{
        margin-top: 4px;
    }
    h4,h3,h5{
        color: $netRed;
    }
    &:hover .copertina{
        opacity: 0.2;
        z-index: 0;
        
    }
}
._box{
    padding: 15px;
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
    background: linear-gradient(33deg, rgba(0,0,0,1) 0%, rgba(221,176,33,1) 71%); 
    
    left: 11px;
    h6{
        font-size: 20px;
        font-weight: 500;
    }
}
</style>