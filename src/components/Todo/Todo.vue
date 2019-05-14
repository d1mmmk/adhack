<template>
    <ul> 
        <todo-item 
            v-for="(todo, index) in todos"
            :key="index"
            :todo="todo"
            @add-group="$emit('add-group', $event)"
            @add-item="$emit('add-item', $event)"
        ></todo-item>
    </ul>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    name: 'todo',
    components: {TodoItem},
    props: ['todos']
}
</script>