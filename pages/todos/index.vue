<template>
    <div class="container mx-auto py-8 w-1/2">
        <ul class="w-full text-center text-sm font-medium text-gray-900 bg-white rounded-lg border border-gray-200 dark:bg-gray-700 dark:border-gray-600 dark:text-white">
            <Todo v-for="todo in todos" :key="todo.id" :todo="todo"/>
        </ul>
    </div>
</template>

<script setup>
    const {data: todos, refresh} = await useFetch('http://localhost:8000/api/todos');
    refresh();
</script>

<style scoped>

</style>