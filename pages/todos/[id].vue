<template>
    <div class="container mx-auto w-1/2 py-8">
        <Title>Edit Todo</Title>

        <form action="#" @submit.prevent="editTodo">
            <div class="mb-6">
                <input type="text" id="description" v-model="description" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="description" required="">
            </div>
            <div class="col-span-6 sm:col-span-3 mb-6">
                <label for="project" class="block text-sm font-medium text-gray-700">Project</label>
                <select id="project" name="project" v-model="project_id" autocomplete="country-name" class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm">
                    <option v-for="p in projects" :value="p.id" :key="p.id">{{p.name}}</option>
                </select>
            </div>
            <div class="flex items-start mb-6">
                <div class="flex items-center h-5">
                    <input id="state" type="checkbox" v-model="state" class="w-4 h-4 bg-gray-50 rounded border border-gray-300 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800">
                </div>
                <label for="state" class="ml-2 text-sm font-medium text-gray-900 dark:text-gray-300">Done</label>
            </div>
            <button type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Submit</button>
        </form>

    </div>
</template>

<script setup>

    const isLoading = ref(false); // not yet implemented
    const route = useRoute();
    const router = useRouter();

    const {data: todo} = await useFetch(`http://localhost:8000/api/todos/${route.params.id}`);
    const {data: projects} = await useFetch(`http://localhost:8000/api/projects/`);

    const description = useState(() => todo._value.description);
    const state = useState(() => todo._value.state === 'Done');
    const project_id = useState(() => todo._value.project_id);


    async function editTodo() {
        isLoading.value = true;

        const resp = await useFetch(`http://localhost:8000/api/todos/${route.params.id}`, {
            method: 'POST',
            body: {
                description: description.value,
                state: state.value ? 'Done' : 'Todo', // should be enum in db
                project_id: project_id.value
            }
        });

        isLoading.value = false;
        router.push(`/projects/${project_id.value}`)
    }

</script>

<!--<style scoped>-->

<!--</style>-->