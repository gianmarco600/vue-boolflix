<template>
  <div id="app">
    <p>ciao</p>
    <ShowBox/>
  </div>
</template>

<script>
import ShowBox from './components/ShowBox.vue'

export default {
  name: 'App',
  components: {
    ShowBox
  }
}
</script>

<style lang="scss">
@import '@/style/commons.scss';
@import '@/style/vars.scss';

p{
  color: white;
}
</style>
