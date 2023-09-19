<template>
  <div class="home">
    <h2 v-for="(item, index) in configList" :key="index">{{ item.value }}</h2>

    <van-swipe class="my-swipe" :autoplay="1000" indicator-color="white">
      <van-swipe-item v-for="item in bannerList"><img :src="item.picUrl" alt="" class="img"></van-swipe-item>
      <van-swipe-item v-for="item in bannerList"><img :src="item.picUrl" alt="" class="img"></van-swipe-item>
    </van-swipe>

    <div class="box" v-for="item in list">
      <div class="div">
        {{ item.name }}
      </div>
      <div class="div">
        <span class="span">{{ item.address }}</span>
        <span>地图></span>
      </div>
      <div class="div">
        <span class="span">营业时间</span>
        <span>{{ item.openingHours }}</span>
      </div>
      <div class="div">
        <span class="span">联系电话</span>
        <span>{{ item.linkPhone }}</span>
      </div>
    </div>

    <!-- 店家推荐 -->
    <footer class="footer">
      <h2>店家推荐</h2>


      <ul>
        <List v-for="(item, index) in cateList" :key="index" @tiaozhanNav="tiaozhanNav" :item="item" class="listq">
        </List>
      </ul>
    </footer>

  </div>
</template>

<script>
import List from '@/components/List.vue';
export default {
  components: { List },
  data() {
    return {
      bannerList: [],
      list: [],
      configList: [],
      cateList: []
    };
  },
  methods: {
    queryHeader() {
      this.$axios.get('https://api.it120.cc/noodles/config/values?keys=mallName').then(res => {
        // console.log(res);
        this.configList = res.data.data;
      })
    },
    queryList() {
      this.$axios.get('https://api.it120.cc/noodles/banner/list', {
        params: {

        },
      }).then(res => {
        // console.log(res);
        this.bannerList = res.data.data;
      })
    },
    queryFooter() {
      this.$axios.get('https://api.it120.cc/noodles/shop/subshop/list').then(res => {
        // console.log(res.data.data);
        this.list = res.data.data;
      })
    },
    queryCate() {
      this.$axios.get('https://api.it120.cc/noodles/shop/goods/list', {
        params: {
          recommendStatus: 1
        },
      }).then(res => {
        console.log(res.data.data);
        this.cateList = res.data.data;
      })
    },
    tiaozhanNav(id) {
      this.$router.push({
        path: '/detail',
        query: {
          id
        }
      })
    }
  },
  created() {
    this.queryCate();
    this.queryFooter();
    this.queryList();
    this.queryHeader();
  }
};
</script>

<style lang="scss" scoped>
.home {
  margin: 0;
  width: 100vw;
  // height: 100vh;
  // margin-bottom:100px;
  padding-bottom: 50px;
  background-color:antiquewhite;
}

h2 {
  text-align: center;
  // margin-top: 10px;
  margin-bottom: 10px;
}

.img {
  width: 100%;
}

.div {
  width: 100%;
  height: 50px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #ccc;
  color: #777;
  box-sizing: border-box;
  padding: 0 30px;

  .span {
    font-weight: bold;
    font-size: 20px;
    color: #000;
  }
}

.footer {
  margin-top: 20px;

}

ul {
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;

  // margin-bottom:100px;
  .listq {
    width: 40%;
    height: 300px;
    margin: 20px 0;
  }
}</style>