<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item">
                {{ todoItem }}
                <button v-on:click="removeTodo(todoItem, index)">Remove</button>
                <button v-on:click="toggleComplete(index)">Complete</button>
            </li>
        </ul>
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
        }
    },
}
</script>

<style>

</style>