<template>
    <li class="py-2 px-4 w-full rounded-t-lg border-b border-gray-200 dark:border-gray-600" :class="{'bg-green-100':props.todo.state === 'Done', 'bg-red-100':props.todo.state !== 'Done'}">
        <NuxtLink :to="`/todos/${props.todo.id}`">{{props.todo.description}}</NuxtLink>
    </li>
</template>

<script setup>
   const props = defineProps({
       todo: Object
   });
</script>

<style scoped>

</style>