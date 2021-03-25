<template>
    <div>
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <button v-on:click="addTodo">add</button>
        <modal v-if="showModal" @close="showModal = false">
            
            <template v-slot:header>
                <h1>Warning!</h1>
            </template>
            <template v-slot:body="slotProps"> <!--  v-slot:슬롯이름="parameter for holding props from child slot"-->
                <div>{{ slotProps.aa }}</div> <!-- parameter.name_of_props 로 참조 -->
            </template>
            <template v-slot:footer>
                <button class="modal-default-button" v-on:click="showModal = false">
                    OK
                </button>
            </template>


            <h1 slot="header">Warning!</h1>
            <div slot="body">You cannot post empty TODO</div>
            <div slot="footer">
                <button class="modal-default-button" v-on:click="showModal = false">
                    OK
                </button>
            </div>
        </modal>
    </div>
</template>

<script>
import Modal from "../common/Modal.vue";

export default {
    data: function() {
        return {
            newTodoItem: "",
            showModal: false,
        };
    },
    methods: {
        addTodo: function() {
            if (this.newTodoItem !== "") {
                this.$emit('addTodoItem', this.newTodoItem)
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput: function() {
            this.newTodoItem = '';
        }
    },
    components: {
        modal: Modal,
    }
};
</script>

<style>

</style>