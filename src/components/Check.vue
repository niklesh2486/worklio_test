<template>
    <span>
        <img class="check" src="../assets/check.svg" />
    </span>
</template>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
    name: 'Check',
    props: {
        itemName: String,
    },
    setup() {  
        return {    
        }
    },
});
</script>

<style>

</style>