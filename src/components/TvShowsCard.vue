<template>
    <div class="_box">
        <div class="risultatoTS film "> 
            <h3>Titolo:</h3>
            {{risultatoTS.name}}
            <h4>titolo originale:</h4>
            {{risultatoTS.original_name}}
            <h4>lingua:</h4>
            <country-flag :country='getLang(risultatoTS.original_language)' size='normal'/> 
            <h5>rating:</h5>
            {{risultatoTS.vote_average}}
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
            queryOutput:''
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
        }
    }
}

</script>

<style lang="scss" scoped>
@import '@/style/commons.scss';
@import '@/style/vars.scss';

.risultatoTS{
    background-color: rgb(31, 31, 31);
    color: white;
    height: 100%;
    // text-align: center;
    padding: 15px;
    // margin: 15px;
    h4,h5{
        margin-top: 10px;
    }
    h4,h3,h5{
        color: $netRed;
    }
}
._box{
    padding: 15px;
}
</style>