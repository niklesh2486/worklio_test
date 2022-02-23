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
import { defineComponent } from 'vue';
// import SearchBar from './SearchBar.vue';
import ItemsList from './ItemsList.vue';
// import Sort from './Sort.vue';

export default {
    name: 'MainPage',
    components: {
        // SearchBar,
        ItemsList,
        // Sort,
    },
    setup() {
        return;
    },
}
</script>

<style>

</style>