<template>
  <div id="app">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
      <!-- v-on:하위 컴포넌트로부터 올라온 이벤트 속성="현재 컴포넌트의 이벤트 핸들러" -->
      <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
      <!-- v-bind:하위 컴포넌트로 내릴 props 속성="현재 컴포넌트의 데이터 속성" -->
      <TodoFooter v-on:removeAllItems="clearAll" v-on:shuffleItems="shuffleList"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue"
import TodoFooter from "./components/TodoFooter.vue"
import TodoList from "./components/TodoList.vue"
import TodoInput from "./components/TodoInput.vue"
import _ from 'lodash';

export default {
    components: {
        "TodoHeader": TodoHeader,
        "TodoFooter": TodoFooter,
        "TodoList": TodoList,
        "TodoInput": TodoInput,
    },
    data: function() {
        return {
            todoItems: []
        }
    },
    methods: {
        addOneItem: function(todoItem) {
            let obj = {completed: false, item: todoItem}
            localStorage.setItem(todoItem.stringify, JSON.stringify(obj));
            this.todoItems.push(obj);
        },
        removeOneItem: function(todoItem, index) {
            localStorage.removeItem(todoItem.item);
            this.todoItems.splice(index, 1)
        },
        toggleOneItem: function(index) {
            // todoItem.completed = !todoItem.completed;
            this.todoItems[index].completed = !this.todoItems[index].completed;
        },
        clearAll: function() {
            this.todoItems = [];
            localStorage.clear();
        },
        shuffleList: function() {
            this.todoItems = _.shuffle(this.todoItems);
        }
    },
    created: function() {
        if (localStorage.length > 0) {
            for (let i=0; i < localStorage.length; i++) {
                if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                }
            }
        }
    },

}

</script>

<style>
    body {
        text-align: center;
        background-color: #f6f6f6;
    }

    input {
        border-style: groove;
        width: 200px;
    }

    button {
        border-style: groove;

    }

    .shadow {
        box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
    }
</style>
