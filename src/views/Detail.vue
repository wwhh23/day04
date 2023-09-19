<template>
    <div class="detail">
        <h2>
            <a href="../views/HomeView.vue">&lt;</a>
            <span>商品详情</span>
        </h2>
        <div class="box">
            <h3>{{ detailList.name }}</h3>
            <img :src="detailList.pic" alt="" class="img">
            <p class="p1">$ {{ detailList.originalPrice }}</p>
            <p class="p2">
                <span>购买数量</span>
                <Num :detailList="detailList"></Num>
            </p>
            <p class="p3">
                <van-button type="primary">去结算</van-button>
                <van-button type="danger" @click="add">加入购物车</van-button>
            </p>
        </div>
    </div>
</template>

<script>
import Num from '@/components/Num.vue';
export default {
    components:{Num},
    data() {
        return {
            id: this.$route.query.id,
            detailList: {},
            shops: JSON.parse(localStorage.getItem('shops')) || [],
        };
    },
    methods: {
        queryList() {
            this.$axios.get('https://api.it120.cc/noodles/shop/goods/detail', {
                params: {
                    id: this.id
                },
            }).then(res => {
                console.log(res.data.data);
                this.detailList = res.data.data.basicInfo;
            })
        },
        add() {
            let foo = this.shops.find(item => item.id == this.detailList.id);
            if (foo) {
                foo.num++
            }
            else {
                this.shops.push({
                    ...this.detailList,
                    num: 1,
                    flag: false
                });
            }
            // this.$router.push({
            //     name: 'cart'
            // })
        }
    },
    created() {
        console.log(this.id);
        this.queryList();
    },
    watch: {
        shops: {
            deep: true,
            handler(val) {
                localStorage.setItem('shops', JSON.stringify(val));
            }
        }
    }
};
</script>

<style lang="scss" scoped>
.detail {
    width: 100%;
    height: 100vh;
    background-color: antiquewhite;
    padding-top: 10px;
}

h2 {
    width: 60%;
    display: flex;
    justify-content: space-between;

    a {
        color: #000;
        margin-left: 20px;
    }
}

.box {
    width: 100%;

    h3 {
        font-size: 23px;
        margin-left: 50px;
        margin-top: 30px;
        margin-bottom: 20px;
    }

    .img {
        width: 100%;
    }

    .p1 {
        color: #f00;
        font-weight: bold;
        margin-left: 30px;
        margin-top: 20px;
        font-size: 22px;
    }

    .p2 {
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 60px;
        box-sizing: border-box;
        padding: 0 20px;
    }

    .p3 {
        display: flex;
        justify-content: space-around;
        align-items: center;
        width: 100%;
        margin-top: 20px;
    }
}</style>