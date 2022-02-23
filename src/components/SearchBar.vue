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

<style lang="scss">
@import "../sass/_color.scss";
    .search-bar{
        position: relative;
        margin: 30px 0;
        input{
            display: block;
            width: 100%;
            padding: 0.375rem 0.75rem;
            color: black;
            background-color: white;
            background-clip: padding-box;
            border: 1px solid grey;
            line-height: 1.5;
            &:focus{
                box-shadow: none;
                outline: none;
            }
        }
        button{
            border: none;
            padding: 9px 12px;
            background-color: blue;
            cursor: pointer;
            position: absolute;
            right: 0;
            top: 0;
        }
        .btn-disable{
            background-color: $lightgrey;
            color: black;
            cursor: not-allowed;
        }
    }
</style>