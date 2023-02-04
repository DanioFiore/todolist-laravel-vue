<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item-form @reload-list="getList"></add-item-form>
        </div>
        <list-view @reload-list="getList" :items="items"></list-view>
    </div>
</template>

<script>
import axios from 'axios';
import AddItemForm from './AddItemForm.vue';
import ListView from './ListView.vue';

export default {
    components: {
        AddItemForm,
        ListView,
    },

    emits: [
        'reloalist',
    ],

    data() {
        return {
            items: [],
        }
    },

    methods: {
        getList() {
            axios.get('api/items')
            .then(res=> {
                this.items = res.data;
            }).catch(err=> {
                console.log(err);
            })
        },
    },

    created() {
        this.getList();
    }
}
</script>

<style scoped>
.todoListContainer {
    width: 350px;
    margin: auto;
}

.heading {
    background: #e6e6e6;
    padding: 10px;

}

.title {
    text-align: center;
}
</style>