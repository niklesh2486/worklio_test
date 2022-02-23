<template>
    <div class="container">
        <div class="left-container">
            <div class="searchbar-conainer">
                <SearchBar @addItemsList="addItems" />
            </div>
            <div class="list-conainer">
                <ItemsList 
                    ref="ItemsList"
                />
            </div>
        </div>
        <div class="right-container">
            <div class="sort-conainer">
                <!-- <Sort /> -->
            </div>
        </div>
    </div>
</template>

<script>
import { defineComponent, ref } from 'vue';
import SearchBar from './SearchBar.vue';
import ItemsList from './ItemsList.vue';
// import Sort from './Sort.vue';



export default defineComponent({
    name: 'MainPage',
    components: {
        SearchBar,
        ItemsList,
        // Sort,
    },
    setup() {
        const listItems = ref([
            { item_name: 'Sun', created_at: new Date() },
            { item_name: 'Moon', created_at: new Date() },
            { item_name: 'Star', created_at: new Date() },
        ]);
        return {
            listItems,
        }
    },
    methods: {
        addItems(){
            let input = document.querySelector('.add-search-input');
            if(input.value.length){
                let items = JSON.parse(localStorage.getItem('setItem'));
                items.push({ item_name: input.value, created_at: new Date() });
                localStorage.setItem('setItem', JSON.stringify(items) );
                input.value = '';
                this.$refs.ItemsList.getListItems();
            }
        }
    },
    created() {
        if(!localStorage.getItem('setItem')){
            window.localStorage.setItem('setItem', JSON.stringify(this.listItems) );
        }
        
    },
});
</script>

<style>

</style>