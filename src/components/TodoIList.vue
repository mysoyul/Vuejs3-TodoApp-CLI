<template>
    <div>
        List
    </div>
</template>

<script setup>
import { ref, onBeforeMount } from 'vue'

const todoItems = ref([])

onBeforeMount(() => {
    console.log('mounted in the composition api!')
    if (localStorage.length > 0) {
        for (var i = 0; i < localStorage.length; i++) {
            const storageValue = localStorage.key(i)
            todoItems.value.push(storageValue)
        }
    }
})

</script>

<style scoped></style>