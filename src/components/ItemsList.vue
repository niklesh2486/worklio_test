<template>
    <div>
        <table border="0" cellspacing="0" cellpadding="0">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Name</th>
                    <th>Created At</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-if="(listItems.length) == 0">
                    <td colspan="4" class="error">
                        No Items Found
                    </td>
                </tr>
                <tr v-for="(listItem, index) in listItems" :key="index">
                    <td>{{ index+1 }}</td>
                    <td>
                        {{ listItem.item_name }}
                        <Check v-if="matchString(searchString, listItem.item_name)"/>
                    </td>
                    <td>
                        {{ getFormat(listItem.created_at) }}
                    </td>
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
import Check from './Check.vue';
import _ from "lodash";

export default defineComponent({
    name: 'ItemsList',
    props: {
        searchString: String,
    },
    components: {
        Trash,
        Check,
    },
    setup() {
        let listItems = ref([]);
        let sortBy = ref('item_name');

        return {
            listItems,
            sortBy,
        }
    },
    methods: {
        getListItems(sortby = null) {
            if(sortby)
            {
                this.sortBy = sortby;
            }
            let items = JSON.parse(localStorage.getItem('setItem'));
            this.sortItems(items, this.sortBy);
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
        },
        matchString(a, b){
            if(_.lowerCase(a) == _.lowerCase(b)){
                return true;
            }
            return false;
        },
        sortItems(items, sortby) {
            items.sort(function(a,b){
                if(sortby == 'item_name')
                    return a.item_name.localeCompare(b.item_name);
                else
                    return new Date(b.created_at) - new Date(a.created_at);
            });
        },
    },
    mounted() {
        this.getListItems();
    },
});
</script>

<style lang="scss">
@import "../sass/_color.scss";
    table{
        width: 100%;
        border: 0;
        thead{
            th{
                padding: 8px;
                background-color: $cyan-blue;
                border: 0;
                text-align: left;
                &:nth-child(1){
                    width: 75px;
                }
                &:nth-child{
                    width: 75px;
                }
            }
        }
        tbody{
            tr{
                &:hover{
                   img.trash{
                       display: block;
                   } 
                }
                td{
                    padding: 15px 8px;
                    background-color: $white;
                    border-bottom: 1px solid lightgrey;
                    img.trash{
                        cursor: pointer;
                        display: none;
                    }
                }
                td.error{
                    background-color: $not-found;
                    color: $warning;
                    text-align: center;
                }
            }
        }
    }
</style>