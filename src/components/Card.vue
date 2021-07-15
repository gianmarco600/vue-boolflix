<template>
    <div class="_box">
        <div class="risultato"> 
            <h3 class="mt_4">Titolo: <span>{{risultato.name || risultato.title}}</span> </h3>
            
            <h4>titolo originale: <span>{{risultato.original_name || risultato.original_title}}</span> </h4>
            
            <div class="row hustify-content-start align-items-center"> 
                <h4 class="col">lingua:</h4>     
                <country-flag class="flag col" :country='getLang(risultato.original_language)' size='normal' :alt="risultato.original_language"/> 
            </div>
            
            <div class="rating ">
                <h5 class="rate">rating:</h5>
                    <i v-for="i in ((Math.ceil(risultato.vote_average))/2)" :key="i" class="fa fa-star full" ></i> 
            </div> 
            <div class="cast">
                <h5>info</h5> 
                <div class="dettagli">
                    <h6>Cast:</h6>
                    <span v-for="(item, index) in Cast" :key="index">{{item}}</span>
                    <h6>Genere:</h6>
                    <span v-for="(item, k) in generiRisultato" :key="k" >{{item}}</span>
                    
                </div>
            </div>
            
            

            <h5>overview: <span>{{risultato.overview.slice(0, 75) + '...'}}</span></h5>
            
            <img v-if="!posterCheck(risultato.poster_path)" class="copertina" :src="imgPATH + 'w500' + risultato.poster_path" :alt="risultato.name || risultato.title">
            <div v-else  class="copertina _bg row align-items-center"><h6>{{risultato.name || risultato.title}}</h6></div>
        </div>
    </div>
</template>

<script>
import CountryFlag from 'vue-country-flag';
import axios from 'axios';

export default {
    name:"Card",
    props:[
        'risultato',
        'listaGeneri'
        ],
    components: {
        CountryFlag
    },
    mounted(){
        if( this.listaGeneri != [] )
        this.getCast(this.risultato);
        this.translateGenere();
    },
    data(){
        return{
            queryOutput:'',
            imgPATH: 'https://image.tmdb.org/t/p/',
            Cast:'',
            generiRisultato:[]
            

        }
    },
    methods:{
        getLang(sigla){
            
            let country = sigla;
            if(country == 'en'){
                country = 'us';
            }
            
            return country
        },
        posterCheck(comp){
            
            if (comp == null ){
                return true
            }
            return false
        },
        getCast(risultato){
            if(risultato.title != null){
                let movieCastURL = 'https://api.themoviedb.org/3/movie/'+ risultato.id +'/credits?api_key=37810146412a45c0824ff15ce4b214ba';
                axios
                    .get(movieCastURL, {
                        params: {
                            api_key : '37810146412a45c0824ff15ce4b214ba',
                        }
                    })   
                    .then(res => {
                        let array = [];
                        for(let i = 0; i < 5; i++){
                            array.push(res.data.cast[i].name);
                        }
                        this.Cast = array;
                        
                    })
                    .catch((error) => {
                    console.log('Errore api cast movie : ' + error);
                    });
                    
                return true
            }
            else{
                if(risultato.name != null){
                    let movieCastURL = 'https://api.themoviedb.org/3/tv/'+ risultato.id +'/credits?api_key=37810146412a45c0824ff15ce4b214ba';
                    axios
                        .get(movieCastURL, {
                            params: {
                                api_key : '37810146412a45c0824ff15ce4b214ba',
                            }
                        })   
                        .then(res => {
                            let array = [];
                            for(let i = 0; i < 5; i++){
                                array.push(res.data.cast[i].name);
                            }
                            this.Cast = array;
                            
                        })
                        .catch((error) => {
                        console.log('Errore api cast tv : ' + error);
                        });
                    return true
                }
            }
        },
        translateGenere(){
            
            this.generiRisultato = this.listaGeneri.map(this.pesca);
            console.log('generi' + this.generiRisultato[0]);
            
        },
        pesca(elem){
            
            for( let i = 0; i < this.risultato.genre_ids.length - 1; i++){
                if(elem.id == this.risultato.genre_ids[i]){
                    return elem.name
                }
            }
        }
    }
}

</script>

<style lang="scss" scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css";
@import '@/style/commons.scss';
@import '@/style/vars.scss';

.rating{
    width: 100%;
}



.rate{
    float: left;
}

.star{
    margin: 0 5px;
    float: left;
    vertical-align: bottom;
    width: 10px;
    height: 10px;
    font-size: 10px;
}

.risultato > i{
    color: yellow;

}

.risultato{
    background-color: rgba(31, 31, 31, 0.52);
    color: white;
    height: 100%;
    // text-align: center;
    overflow-y:auto ;
    padding: 40px 15px 15px 15px;
    position: relative;
    // z-index: 1;
    overflow: hidden;
    // margin: 15px;
    text-align: left;
    .flag{
        display: inline-block;
        padding: 0;
        // margin-left: -60%;
    }
    h6{
        margin-top: 10px;
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
        font-size: 12px;
        display: block;
        text-transform: capitalize;
        flex-grow: 0;
        text-align: left;
    }
    &:hover .copertina{
        opacity: 0.2;
        // z-index: 0;
        
    }
    span{
        color: white;
        font-size: 11px;
        font-weight: 100;
        display: block;
    }
    .cast{
        position: absolute;
        left: 0;
        right: 0;
        width: 100%;
        top: 0;
        background-color: red;
        padding: 10px;
        z-index: 99999;
        display: none;
        height: 40px;
        transition: display 0.2;
        .dettagli{
            display: none;
            background-color: rgb(31, 31, 31);
            padding: 6px;
        }
        &:hover .dettagli{
            display: block;
            
            border-radius: 3px;
        }
        h5{
            color: black;
        }
        
    
    }
    &:hover .cast{
        display: block;
        transition: display 0.2;
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
    width: 100%;
    background: rgb(0,0,0);
    background: linear-gradient(33deg, rgba(0,0,0,1) 0%, rgba(229,9,20,1) 71%); 
    padding: 10px;
    left: 10px;
    h6{
        font-size: 20px;
        font-weight: 500;
    }
    
}





</style>