<template>
  <div class="risultato film "> 
      <h3>Titolo:</h3>
      {{risultato.title}}
      <h4>titolo originale:</h4>
      {{risultato.original_title}}
      <h4>lingua:</h4>
      {{risultato.original_language}}  
      <h5>rating:</h5>
      {{risultato.vote_average}}
  </div>
</template>

<script>
export default {
    name:'MovieCard',
    props:[
        'risultato',
    ],
    data(){
        return{
            queryOutput:''
        }
    },
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
        color: #E50914;
    }
}
.film{
    width: calc(100% / 4 - 30px);

}

</style>