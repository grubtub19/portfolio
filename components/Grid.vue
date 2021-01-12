<template>
    <div class="grids">
        <div class="grid-item" v-for="item in gridArray" :key="item"
        :class="'grid-' + item">
        </div>
    </div>
</template>

<script>
export default {
    props: 
        ['gridArray']
}
</script>

<style lang='scss'>
.grids {
    transition: margin-left 0.8s cubic-bezier(0.37, -0.04, 0.25, 1);
    margin-left: 0;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;

    .grid-item {
        position: absolute;
        display: block;
        height: 100%;
        min-height: 100vh;
        width: 1px;
        background-color: $line-color;
        opacity: 5%;

        &.grid-0 {
            left: $grid-0;
        }
        &.grid-1 {
            left: $grid-1;
        }
        &.grid-2 {
            left: $grid-2;
        }
        &.grid-3 {
            left: $grid-3;
        }
        &.grid-4 {
            left: $grid-4;
        }
        &.grid-5 {
            left: $grid-5;
        }
        &.grid-6 {
            left: $grid-6;
        }
        &.grid-7 {
            left: $grid-7;
        }
        &.grid-8 {
            left: $grid-8;
        }
        &.grid-9 {
            left: $grid-9;
        }
        &.grid-10 {
            left: $grid-10;
        }
        &.grid-11 {
            left: $grid-11;
        }
    }
}
</style>