<template>
    <div>
        <van-tabbar route active-color="#e44545" inactive-color="#ababb7">
            <van-tabbar-item replace to="/" icon="wap-home">首页</van-tabbar-item>
            <van-tabbar-item replace to="/about" icon="like">菜单</van-tabbar-item>
            <van-tabbar-item replace to="/cart" icon="shopping-cart">购物车</van-tabbar-item>
            <van-tabbar-item replace to="/my" icon="friends">我的</van-tabbar-item>
        </van-tabbar>
    </div>
</template>

<script>
export default {
    data() {
        return {};
    },
    methods: {},
};
</script>

<style lang="scss" scoped></style>