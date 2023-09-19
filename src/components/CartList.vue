<template>
    <div>
        <van-row type="flex" align="center">
            <van-col span="2">
                <van-checkbox v-model="item.flag" @change="fx"></van-checkbox>
            </van-col>
            <van-col span="20">
                <van-swipe-cell>
                    <van-card :price="item.originalPrice" :title="item.name" :thumb="item.pic">
                        <template #footer>
                            <van-stepper v-model="item.num" />
                        </template>
                    </van-card>
                    <template #right>
                        <van-button square text="删除" type="danger" class="delete-button" />
                    </template>
                </van-swipe-cell>
            </van-col>
        </van-row>
    </div>
</template>

<script>
export default {
    props: ["item"],
    data() {
        return {};
    },
    methods: {
        fx() {
            this.$emit('fx');
        }
    },
};
</script>

<style lang="scss" scoped>
.delete-button {
    height: 100%;
}
</style>