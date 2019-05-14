<template>
    <span>
        <button class="btn" @click="toggleShow">
            <span v-if="!show">+</span>
            <span v-if="show">-</span>
        </button>
        <div v-show="show">
            <input v-model="name" @keydown="keydown" ref="name" />
            <button class="btn" @click="addGroup" title="Shift + Enter">+group</button>
            <button class="btn" @click="addItem" title="Enter">+item</button>
        </div>
    </span>
</template>

<script>

export default {
    name: 'todo-item-add',
    props: ['parent'],
    data: function(){
        return {
            name: '',
            show: false
        }
    },
    methods: {
        keydown: function(e){
            if (e.keyCode === 13) {
                if (e.shiftKey) {
                    this.addGroup();
                } else {
                    this.addItem();
                }
            }
        },
        toggleShow: function(){
            this.show = !this.show;

            if (this.show){
                setTimeout(function(){
                    this.$refs.name.focus();
                }.bind(this))
            }
        },
        addGroup: function(){
            this.$emit('add-group', {name: this.name, parent: this.parent});
            this.name = '';
        },
        addItem: function(){
            this.$emit('add-item', {name: this.name, parent: this.parent});
            this.name = '';
        }
    }
}
</script>

<style>
    .btn {
        outline: none;
        cursor: pointer;
        margin: 0 0 0 1em;
        line-height: 1em;
        border: 1px solid gray;
        border-radius: 5px;
    }
    input {
        outline: none;
        line-height: 1em;
        padding: 0;
        margin: 0;
    }
</style>