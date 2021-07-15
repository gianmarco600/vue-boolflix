<template>
  <header>
      <div class="_container">
          <div class="nav row justify-content-between align-items-centers">
              <div class="col _logo">boolflix</div>
              <div class="col search_box">
                <label  for="search">Cerca</label>
                <input 
                    v-model="input"
                    placeholder="Es: 'matrix'"
                    @keyup="$emit('input' , input )"
                    id="search" class="search " type="text">
                
                </div>
                
          </div>
      </div>
  </header>
</template>

<script>
export default {
    name:'Header',
    data(){
        return{
            input:''
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/style/commons.scss';
@import '@/style/vars.scss';


header{
    width: 100%;
    height: 100px;
    background-color: rgb(32, 32, 32);
}

._container{
    height: 100%;
}

._logo{
    width: 20%;
    align-self: center;
    display: inline;
    font-size: 50px;
    text-transform: uppercase;
    font-weight: 100;
    color: $netRed;
}

.nav{
    height: 100%;
    width: 100%;
    align-items: center;
}

.search_box{
    height: 50px;
    width: 400px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    font-weight: 700;
    color: #3a3a3a;
    font-size: 20px;
    &:hover .search{
        width: 300px;
        transition: width 0.7s;
        background-color: #3a3a3a;
    }
}

.search{
    width: 0;
    transition: width 0.7s;
    flex-grow: 0;
    background-color: #22222200;
    box-sizing: content-box;
    border: 5px solid $netRed;
    height: 60%;
    border-radius: 20px;
    transition: 0.5s;
    color: white;
    margin-left: 40px;
    padding: 1px 15px;
    
    &:hover{
        transform: scale(1.05,1.05);
        transition: 0.5s;
    }
}
</style>