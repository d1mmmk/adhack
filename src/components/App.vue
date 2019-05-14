<template>
    <div id="app"><todo 
        :todos="todos"
        
        @add-group="addGroup"
        @add-item="addItem"
        /></div>
</template>

<script>
import todo from './Todo/Todo.vue';

export default{
    name: 'App',
    components: {todo},
    data: function(){
        return {todos: window.todosData}
    },
    methods: {
        addGroup: function(params){
            let parent = params.parent || this.todos,
                name = params.name || 'new group';

            parent.items.push({
                type: 'group',
                name: name,
                items: []
            })
        },
        addItem: function(params){
            let parent = params.parent || this.todos,
                name = params.name || 'new item';
                
            parent.items.push({
                type: 'item',
                done: false,
                name: name,
            })
        }
    }
};
</script>