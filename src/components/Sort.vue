<template>
    <div>
        <div class="radio-outer">
            <label for="item_name">Sort by value</label>
            <input id="item_name" type="radio" name="sorBy" value="item_name" checked="checked" @change="$emit('sort', $event)" />
        </div>
        <div class="radio-outer">
            <label for="created_at">Sort by added date</label>
            <input id="created_at" value="created_at" type="radio" name="sorBy" @change="$emit('sort', $event)" />
        </div>
    </div>
    
</template>

<script>
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'Sort',
    setup() {
        return;
    },
});
</script>

<style>

</style>