<template>
    <div>
        <table border="">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Name</th>
                    <th>Created At</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(listItem, index) in listItems" :key="index">
                    <td>{{ index+1 }}</td>
                    <td>{{ listItem.item_name }}</td>
                    <td>{{ getFormat(listItem.created_at) }}</td>
                    <td>
                        <Trash 
                            :item-name="listItem.item_name"
                            @deleteNode="deleteNode"
                        />
                        </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import { defineComponent, ref } from 'vue';
import { formatDistance } from 'date-fns'
import Trash from './Trash.vue';

export default defineComponent({
    name: 'ItemsList',
    components: {
        Trash,
    },
    setup() {
        let listItems = ref([]);
        return {
            listItems,
        }
    },
    methods: {
        getListItems() {
            let items = JSON.parse(localStorage.getItem('setItem'));
            this.listItems = items;
        },
        getFormat(date) {
            return formatDistance( new Date(date),new Date(),{ addSuffix: true });
        },
        deleteNode(val) {
            let filtered = this.listItems.filter(item => item.item_name !== val);
            window.localStorage.setItem('setItem', JSON.stringify(filtered) );
            this.listItems = filtered;
        },
        sortedList(filterData){
            this.listItems = filterData;
        }
    },
    mounted() {
        this.getListItems();
    },
});
</script>

<style>

</style>