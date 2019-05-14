<template>
    <li>
        <span v-if="!isGroup">{{todo.name}}</span> 
        <strong v-if="isGroup">{{todo.name}}</strong>
        <todo-item-add  
            v-if="isGroup"
            :parent="todo"
            @add-group="$emit('add-group', $event)"
            @add-item="$emit('add-item', $event)"
        />
        <ul v-if="hasChild">
            <todo-item 
                v-for="(todo, index) in todo.items"
                :key="index"
                :todo="todo"
                @add-group="$emit('add-group', $event)"
                @add-item="$emit('add-item', $event)"
            ></todo-item>
        </ul>
    </li> 
</template>

<script>
import TodoItemAdd from './TodoItemAdd.vue';

export default {
    name: 'todo-item',
    props: ['todo'],
    components: {TodoItemAdd},
    created: function(){
    },
    computed: {
        isGroup: function () {
            return this.todo.type && this.todo.type === 'group'
        },
        hasChild: function() {
            return !!(this.todo.items && this.todo.items.length);
        }
    }
}
</script>