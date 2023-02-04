<template>
    <div v-for="(item, index) in items" :key="index">
        <list-item @item-changed="$emit('reload-list')" :item="item" class="item"></list-item>
    </div>
</template>

<script>
import ListItem from './ListItem.vue';
export default {
    props: ['items'],
    components: {
        ListItem
    },
    emits: [
        'reload-list'
    ]
}
</script>

<style scoped>
.item {
    background:  #e6e6e6;
    padding: 5px;
    margin-top: 5px;
}
</style>