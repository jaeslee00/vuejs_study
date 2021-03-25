<template>
    <div>
        <button v-on:click="removeAll">Remove All</button>
    </div>
</template>

<script>
export default {
    methods: {
        removeAll: function() {
            this.$emit('removeAllItems');
        }
    }
}
</script>

<style>

</style>