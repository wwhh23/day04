<template>
    <div>
        <van-stepper v-model="detailList.seckillBuyNumber" min="1" />
    </div>
</template>

<script>
export default {
    props: ["detailList"],
    data() {
        return {};
    },
    methods: {},
};
</script>

<style lang="scss" scoped></style>