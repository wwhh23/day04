<template>
  <div id="app">
    <router-view />
    <Tarbar></Tarbar>
  </div>
</template>
<script>
import Tarbar from './components/Tarbar.vue';
export default {
  components:{Tarbar},
}
</script>
<style lang="scss">
* {
  padding: 0;
  margin: 0;
  // padding-bottom:100px;
  // margin-bottom:100px;
}

li {
  list-style: none;
}

a {
  text-decoration: none;
}
</style>
