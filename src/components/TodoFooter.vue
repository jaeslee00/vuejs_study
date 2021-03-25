<template>
    <div>
        <button v-on:click="removeAll">Remove All</button>
        <button v-on:click="shuffleTodo">Shuffle</button>
    </div>
</template>

<script>
export default {
    methods: {
        removeAll: function() {
            this.$emit('removeAllItems');
        },
        shuffleTodo: function() {
            this.$emit("shuffleItems")
        }
    }
}
</script>

<style>

</style>