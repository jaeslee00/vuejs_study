<template>
    <div>
        <transition-group name="list" tag="ul">
            <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item">
                {{ todoItem }}
                <button v-on:click="removeTodo(todoItem, index)">Remove</button>
                <button v-on:click="toggleComplete(index)">Complete</button>
            </li>
        </transition-group>
    </div>
</template>
<script>
export default {
    props: ["propsdata"],
    methods: {
        removeTodo: function(todoItem, index) {
            this.$emit("removeItem", todoItem, index);
        },
        toggleComplete: function(index) {
            this.$emit("toggleItem", index)
        },
    },
}
</script>

<style>
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active, .list-leave-active {
  transition: all 0.5s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateX(100px);
}
.list-move {
  transition: transform 1s;
}
</style>