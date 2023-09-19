<template>
    <div class="cart">
        <h1>购物车</h1>
        <h4>
            <span class="span1">您选购的商品</span>
            <span class="span2" @click="activeFn">{{ active ? '编辑' : '完成' }}</span>
        </h4>
        <CartList v-for="(item, index) in shops" :key="index" :item="item" @fx="fx"></CartList>

        <van-button type="danger" @click="dels" class="button">{{ active ? '去结算' : '批量删除' }}</van-button>


        <Footer class="footer" :sum="sum" :shops="shops" @qx="qx"></Footer>



    </div>
</template>

<script>
import Footer from '@/components/Footer.vue';
import CartList from '@/components/CartList.vue';
export default {
    components: { CartList, Footer },
    data() {
        return {
            shops: JSON.parse(localStorage.getItem('shops')) || [],
            change: false,
            active: true,
        };
    },
    methods: {
        activeFn(){
            if(this.active == true){
                this.active = false;
            }
            else{
                this.active = true;
            }
        },
        dels() {
            this.shops = this.shops.filter((item) => {
                return item.flag == false
            })
        },
        qx(val) {
            this.change = val;
            // this.shops.forEach((item) => {
            //     item.flag = this.change;
            // })
        },
        fx() {
            // console.log('111');
            this.change = this.shops.every(item => item.flag);
        }
    },
    computed: {
        sum() {
            let a = 0;
            this.shops.forEach(item => {
                if (item.flag) {
                    a += item.num * item.originalPrice;
                }
            })
            return a
        }
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
.button {
    margin-top: 30px;
    margin-left: 50px;
}

h1 {
    text-align: center;
}

.cart {
    width: 100%;
    height: 100vh;
    background-color: antiquewhite;
    // margin-bottom:50px;
}

h4 {
    width: 100%;
    height: 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-sizing: border-box;
    padding: 0 40px;

    .span2 {
        color: #777;
    }
}
</style>