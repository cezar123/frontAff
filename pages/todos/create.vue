<template>
    <div class="container mx-auto w-1/2 py-8">
        <Title>Create Todo</Title>
        <ul v-if="errors.length > 0">
            <li>{{err}}</li>
        </ul>
        <form action="#" class="space-y-6" @submit.prevent="createTodo">
            <div>
                <label for="description">Title</label>
                <input type="text" v-model="description" id="description" class="px-2 py-2 w-full shadow rounded mt-2">
            </div>
            <div class="col-span-6 sm:col-span-3">
                <label for="project" class="block text-sm font-medium text-gray-700">Project</label>
                <select id="project" name="project" autocomplete="country-name" class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm">
                    <option v-for="p in projects" value="p.id" :key="p.id">{{p.name}}</option>
                </select>
            </div>
            <div>
                <button type="submit" class="inline-block bg-blue-600 hover:bg-blue-700 text-white rounded px-4 py-2">Save</button>
                <span v-show="isLoading">Loading...</span>
            </div>
        </form>
    </div>
</template>

<script setup>

    const name = ref('');
    const description = ref('');
    const errors = ref('');
    const isLoading = ref(false);
    const router = useRouter();
    const {data: projects} = await useFetch(`http://localhost:8000/api/projects/`);


    async function createTodo(){
        isLoading.value = true;

        try {
            const resp = await useFetch(`http://localhost:8000/api/todos/`, {
                method: 'POST',
                body: {
                    description: description.value,
                    project_id: project.value,
                }
            });

            isLoading.value = false;
            title.value = '';
            router.push('/todos');

        } catch (e) {
            errors.value = Object.values(e.data.errors).flat();
            isLoading.value = false;
        }

    }

</script>

<style scoped>

</style>