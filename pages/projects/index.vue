<template>
    <div class="container mx-auto w-1/2 py-8 flex items-center justify-center">
        <ul class="w-full text-center text-sm font-medium text-gray-900 bg-white rounded-lg border border-gray-200 dark:bg-gray-700 dark:border-gray-600 dark:text-white">
            <Project v-for="project in projects" :key="project.id" :project="project" />
        </ul>
    </div>
</template>

<script setup>
    const {data:projects, refresh} = await useFetch('http://localhost:8000/api/projects');
    refresh();
</script>