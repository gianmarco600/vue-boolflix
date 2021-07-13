<template>
    <div class="_box">
        <div class="risultatoM film "> 
            <h3>Titolo:</h3>
            {{risultatoM.title}}
            <h4>titolo originale:</h4>
            {{risultatoM.original_title}}
            <h4>lingua:</h4>
            <country-flag :country='getLang(risultatoM.original_language)' :alt="risultatoM.original_language" size='normal'/> 
            <h5>rating:</h5>
            {{risultatoM.vote_average}}
            <h5>overview</h5>
            {{risultatoM.overview.slice(0, 90) + '...'}}
            <img class="copertina" :src="imgPATH + 'w500' + risultatoM.poster_path" :alt="risultatoM.title">
        </div>
    </div>
</template>

<script>

import CountryFlag from 'vue-country-flag';

export default {
    name:'MovieCard',
    props:[
        'risultatoM',
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
        getLang(film){
            
            let country = film.slice(0,2);
            if(country == 'en'){
                country = 'us';
            }
            // console.log(country);
            return country
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/style/commons.scss';
@import '@/style/vars.scss';

.risultatoM{
    background-color: rgb(31, 31, 31);
    color: white;
    height: 100%;
    // text-align: center;
    padding: 15px;
    // margin: 15px;
    position: relative;
    h4,h5{
        margin-top: 10px;
    }
    h4,h3,h5{
        color: $netRed;
    }
    &:hover .copertina{
        opacity: 0.2;
        
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
// .film{
//     width: calc(100% / 4 - 30px);

// }

</style>