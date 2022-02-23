<template>
    <div class="search-bar">
        <input type="text" class="add-search-input"/>
        <AddButton @handleAdd="handleAdd" />
    </div>
</template>

<script>
import { defineComponent } from 'vue';
import AddButton from './AddButton.vue';

export default defineComponent({
    name: 'SearchBar',
    components: {
        AddButton,
    },
    setup() {
        return;
    },
    methods: {
        handleAdd(){
            this.$emit('addItemsList');
        }
    }

});
</script>

<style>

</style>