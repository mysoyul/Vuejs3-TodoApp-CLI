<template>
    <div>
        <input type="text" v-model="newTodoItem">
        <button>추가</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const newTodoItem = ref("")

</script>

<style scoped></style>