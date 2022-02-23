<template>
    <div class="container">
        <div class="left-container">
            <div class="searchbar-conainer">
                <SearchBar 
                    @addItemsList="addItems"
                    @filter-list="filterList"
                    :add-button="addButton"
                    :search-string="searchString"
                    @reset-list="resetList"
                />
            </div>
            <div class="list-conainer">
                <ItemsList 
                    ref="ItemsList"
                    :search-string="searchString"
                />
            </div>
        </div>
        <div class="right-container">
            <div class="sort-conainer">
                <Sort
                    @sort="callSortItems"
                />
            </div>
        </div>
    </div>
</template>

<script>
import { defineComponent, ref } from 'vue';
import SearchBar from './SearchBar.vue';
import ItemsList from './ItemsList.vue';
import Sort from './Sort.vue';

import _ from "lodash";



export default defineComponent({
    name: 'MainPage',
    components: {
        SearchBar,
        ItemsList,
        Sort,
    },
    setup() {
        let searchString = ref(null);
        let filter = ref(null);
        let addButton = ref(false);
        const listItems = ref([
            { item_name: 'Sun', created_at: new Date() },
            { item_name: 'Moon', created_at: new Date() },
            { item_name: 'Star', created_at: new Date() },
        ]);
        return {
            listItems,
            searchString,
            filter,
            addButton,
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
                this.searchString = null;
                this.$refs.ItemsList.getListItems();
            }
        },
        filterList(value) {
            this.searchString = value;
            let items = JSON.parse(localStorage.getItem('setItem'));
            this.filter = items.filter(item => _.lowerCase(item.item_name).includes(_.lowerCase(value)));
            if(this.filter){
                let match = this.filter.find(item => _.lowerCase(item.item_name) == (_.lowerCase(value)));
                this.$refs.ItemsList.sortedList(this.filter);
                if(match){
                    this.addButton = true;
                }
                else
                {
                    this.addButton = false;
                }
            }
        },
        resetList(){
            this.filter = null;
            this.searchString = null;
            this.addButton = false;
            this.$refs.ItemsList.getListItems();
        },
        callSortItems(event) {
            this.$refs.ItemsList.getListItems(event.target.value);
        }
    },
    created() {
        if(!localStorage.getItem('setItem')){
            window.localStorage.setItem('setItem', JSON.stringify(this.listItems) );
        }
        
    },
});
</script>

<style lang="scss">
.container{
    margin: 0 auto;
    max-width: 1170px;
    padding: 0 15px;
    margin-top: 30px;
    height: 90vh;
    scroll-behavior: smooth;
    overflow-y: scroll;
    .left-container{
        width: 70%;
        float: left;
    }
    .right-container{
        width: 30%;
        float: right;
        margin-top: 90px;
        padding: 0 50px;
    }

}
</style>