<template>
    <div class="todo-item" v-bind:class="{'is-complete': todo.completed }">
        <input type="checkbox" v-on:change="markComplete">
        <p>{{ todo.title }}</p>
        <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </div>
</template>

<script>
export default {
    name: 'TodoItem',
    props: ['todo'],
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed
        }
    },
}
</script>

<style scoped>

    .todo-item {
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px solid #ccc;
        display: flex;
        align-content: center;
    }

    .is-complete {
        text-decoration: line-through;
    }

    p {
        margin-left: 10px;
    }

    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 10px;
        border-radius: 50%;
        cursor: pointer;
        margin-left: auto;
    }

</style>


