<template>
  <div>
    <TodoHeader></TodoHeader>
    <TodoInput @add:todo="addTodo"></TodoInput>
    <TodoIList @remove:todo="removeTodo" @toggle:todo="toggleTodo"></TodoIList>
    <TodoFooter @clear:todo="clearTodo"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoIList from './components/TodoIList.vue'
import TodoFooter from '@/components/TodoFooter.vue'
import { onBeforeMount, reactive } from 'vue'

export default {
  name: 'App',
  components: {
    TodoHeader,
    TodoInput,
    TodoIList,
    TodoFooter
  },
  setup() {
    const todoItems = reactive([]);

    onBeforeMount(() => {
      if (localStorage.length > 0) {
        for (var i = 0; i < localStorage.length; i++) {
          const storageKey = localStorage.key(i)
          const itemJson = localStorage.getItem(storageKey)
          if (itemJson) {
            todoItems.push(JSON.parse(itemJson));
          } //if
        } //for
      } //if
    }) //onBeforeMount

    const addTodo = (todoItemStr) => {
      const todoItemObj = { completed: false, item: todoItemStr };
      //obj => json 변환해서 로컬스토리지에 저장
      localStorage.setItem(todoItemStr, JSON.stringify(todoItemObj));
      todoItems.push(todoItemObj);
    };//addTodo

    const removeTodo = (todoItem, index) => {
      localStorage.removeItem(todoItem)
      todoItems.splice(index, 1)
    }

    const toggleTodo = (todoItem, index) => {
      const { item, completed } = todoItem
      todoItems[index].completed = !completed
      localStorage.removeItem(item)
      localStorage.setItem(item, JSON.stringify(todoItems[index]))
    };

    const clearTodo = () => {
      localStorage.clear()
      todoItems.splice(0)
    }

    return { todoItems, addTodo, removeTodo, toggleTodo, clearTodo };
  }, //setup
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

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
