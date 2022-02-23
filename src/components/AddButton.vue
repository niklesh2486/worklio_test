<template>
    <span class="add-btn">
        <img class="add" @click="$emit('handleAdd')" src="../assets/add.svg" />
    </span>
</template>

<script>
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'AddButton',
    setup() {
        return;
    },

});
</script>

<style lang="scss">
@import "../sass/_color.scss";
    .add-btn{
        position: absolute;
        top: 1px;
        right: 0px;
        padding: 3px 8px 0 8px;
        line-height: 17px;
        cursor: pointer;
        background-color: $cyan-blue;
    }
</style>