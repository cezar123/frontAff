<template>
    <div class="container mx-auto w-1/2 py-8">
        <h3>Todos</h3>
        <ul class="w-full text-center text-sm font-medium text-gray-900 bg-white rounded-lg border border-gray-200 dark:bg-gray-700 dark:border-gray-600 dark:text-white">
            <li v-for="todo in projectWithTodos.todos" :key="todo.id" class="py-2 px-4 w-full rounded-t-lg border-b border-gray-200 dark:border-gray-600">
                <NuxtLink :to="`/todos/${todo.id}`">{{todo.description}}</NuxtLink>
            </li>
        </ul>
    </div>
</template>

<script setup>
    const route = useRoute();
    const {data: projectWithTodos, refresh} = await useFetch(`http://localhost:8000/api/projects/${route.params.id}`);
    refresh();
</script>

<!--<style scoped>-->

<!--</style>-->