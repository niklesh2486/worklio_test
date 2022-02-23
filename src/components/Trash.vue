<template>
    <span>
        <img class="trash" src="../assets/trash.svg" @click="$emit('deleteNode', itemName)" />
    </span>
</template>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
    name: 'Trash',
    props: {
        itemName: String,
    },
    setup() {
        
        return {
            
        }
    },
    methods: {
        
    },
});
</script>

<style>

</style>