<template>
    <div>
        <li  @click="tiaozhanNav(item.id)">
          <img :src="item.pic" alt="" class="img" >
          <h3>{{ item.name }}</h3>
          <p>${{ item.originalPrice }}</p>
        </li>
    </div>
</template>

<script>
export default {
    props:["item"],
 data() {
     return {};
 },
 methods: {
    tiaozhanNav(id){
        this.$emit('tiaozhanNav',id);
    }
 },
};
</script>

<style lang="scss" scoped>
 li{
   
    .img{
      width: 100%;
      height:220px;
    }
    h3{
      font-weight:bold;
      margin-left:30px;
      margin-top:20px;
      margin-bottom:10px;
    }
    p{
      color:#c00;
      margin-left:30px;
      font-weight: bold;
    }
  }
</style>