<template>
    <div class="item">
        <input type="checkbox" v-model="item.completed" @change="updateCheck"/>
        <span :class="[item.completed ? 'completed' : '', 'itemText']">{{
            item.name
        }}</span>
        <button @click="removeItem" class="trashcan">
            <font-awesome-icon icon="trash"></font-awesome-icon>
        </button>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    props: ["item"],

    methods: {
        removeItem() {
            axios.delete("api/item/" + this.item.id, {
                item: this.item,
            })
            .then(res => {
                if(res.status == 200) {
                    this.$emit('item-changed')
                }
            })
            .catch(err=> console.log(err))
        },
    },
    updateCheck() {
        axios.put('api/item/' + this.item.id)
            .then(res => {
                if(res.status == 200) {
                    this.$emit('item-changed')
                }
            })
            .catch(err => console.log(err))
    }
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: #9999;
}

.itemText {
    width: 100%;
    margin-left: 20px;
}
.item {
    display: flex;
    justify-content: center;
    align-items: center;
}

.trashcan {
    background-color: #e6e6e6;
    border: none;
    color: #ff0000;
    outline: none;
}
</style>
