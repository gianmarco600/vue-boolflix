<template>
    <div class="_container text-center">
        <h3 class="cerca">cerca: {{inputQuery}}</h3>
        <div v-if="queryOutputTS != [] || queryOutputM != []" class=" porta_scaffali">
            
            <div v-if='queryOutputM.length != 0'>
                <h2 v-if='queryOutputM.length != 0' class="_label section">Movies</h2>
                <div v-if='queryOutputM.length != 0' class="row scaffale justify-content-start align-items-start">
                    <Card :listaGeneri='listaGeneriM' class="_card" v-for="risultatoM  in queryOutputM" :key="risultatoM.id"  :risultato="risultatoM"/>
                </div>
            </div>
            <div  v-if='queryOutputTS.length != 0'>
                <h2 v-if='queryOutputTS.length != 0' class="_label section">Tv Shows</h2>
                <div class="row scaffale justify-content-start align-items-start" >
                    <Card :listaGeneri='listaGeneriTS' class="_card" v-for="risultatoTS  in queryOutputTS" :key="risultatoTS.id" :risultato="risultatoTS"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>




import Card from '@/components/Card.vue';


export default {
    name:'ShowBox',
    components:{
        Card,
        
    },
    props:{
        queryOutputTS: Array,
        queryOutputM: Array,
        inputQuery: String,
        listaGeneriTS: Array,
        listaGeneriM: Array
    },
}
</script>

<style lang="scss" scoped>
@import '@/style/commons.scss';
@import '@/style/vars.scss';

._container{
    margin-top: 110px;
}

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

.porta_scaffali{
    width: 100%;
}

.scaffale{
    width: 80vw;

    
    padding: 0px 20px;
    display: flex;
    overflow-x: auto;
    // box-sizing: content-box;
    margin: 10px 0 15px 0;
    flex-wrap: nowrap;

    

}

._card{
    padding: 10px;
    width: 12vw ;
    height: calc(9vw * 16 / 9);
    margin: 10px 10px;
    // max-height: 500px;
    &:hover{
        box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
    }
}

.cerca{
    color: white;
    text-align: left;
    margin-left: 40px;
    text-transform: uppercase;
    background-color: #202020;
    display: inline-block;
    
    font-size: 20px;
    padding: 10px;
    border-radius: 10px;
}

._label{
    display: inline-block;
    color: white;
    margin-left: 40px;
    
}
</style>