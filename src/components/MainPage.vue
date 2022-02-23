<template>
    <div class="container">
        <div class="left-container">
            <div class="searchbar-conainer">
                <!-- <SearchBar /> -->
            </div>
            <div class="list-conainer">
                <ItemsList />
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
// import SearchBar from './SearchBar.vue';
import ItemsList from './ItemsList.vue';
// import Sort from './Sort.vue';



export default defineComponent({
    name: 'MainPage',
    components: {
        // SearchBar,
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
    created() {
        if(!localStorage.getItem('setItem')){
            window.localStorage.setItem('setItem', JSON.stringify(this.listItems) );
        }
        
    },
});
</script>

<style>

</style>