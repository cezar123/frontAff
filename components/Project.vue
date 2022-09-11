<template>
    <li class="py-2 px-4 w-full rounded-t-lg border-b border-gray-200 dark:border-gray-600">
        <NuxtLink :to="`/projects/${props.project.id}`">{{props.project.name}}</NuxtLink>
    </li>
</template>

<script setup>
    const name = "Project";
    const props = defineProps({
        project: Object
    });
</script>