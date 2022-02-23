<template>
    <div class="search-bar">
        <input 
            type="text" 
            class="add-search-input"
            @keydown.esc="clearInput()"
            @keydown.enter="handleAdd()"
            v-model="filterValue"
            @input="$emit('filterList', filterValue)"
        />
        <AddButton 
            v-if="searchString"
            @handleAdd="handleAdd"
            :class="[addButton ? 'btn-disable' : '']"
            :disabled="addButton"
        />
    </div>
</template>

<script>
import { defineComponent } from 'vue';
import AddButton from './AddButton.vue';

export default defineComponent({
    name: 'SearchBar',
    props: {
        addButton: Boolean,
        searchString: String,
    },
    emits: ['filterList'],
    components: {
        AddButton,
    },
    setup() {
        let filterValue;
        return{
            filterValue,
        }
    },
    methods: {
        handleAdd(){
            if(!this.addButton){
                this.filterValue ='';
                this.$emit('addItemsList');
            }            
        },
        clearInput(){
            document.querySelector('.add-search-input').value = '';
            this.filterValue ='';
            this.$emit('resetList');
        }
    }

});
</script>

<style>

</style>