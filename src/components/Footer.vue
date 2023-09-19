<template>
    <div>
        <van-submit-bar :price="sum * 100" button-text="批量删除">
            <van-checkbox v-model="checked" @click="qx">全选</van-checkbox>
        </van-submit-bar>
    </div>
</template>

<script>
export default {
    props: ["sum", "shops"],
    data() {
        return {
            checked: false,
        };
    },
    methods: {
        qx() {
            this.shops.forEach(item => item.flag = this.checked);
            this.$emit('qx', this.checked);
        }
    },
};
</script>

<style lang="scss" scoped>
.van-submit-bar {
    bottom: 50px;
}
</style>