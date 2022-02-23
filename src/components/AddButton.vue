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

<style>

</style>