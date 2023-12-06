<template>
    <div>
        {{ newTodoItem }}
        <input type="text" :value="newTodoItem" v-on:input="handleInput">
        <button>추가</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const newTodoItem = ref("")
//"input:todo" 이벤트 정의
const emit = defineEmits(["input:todo"])

const handleInput = (event) => {
    const todoText = event.target.value
    if (!todoText) return
    //이벤트 발생
    emit("input:todo", todoText)
    newTodoItem.value = todoText
}

</script>

<style scoped></style>