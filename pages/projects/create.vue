<template>
    <div class="container mx-auto w-1/2 py-8">
        <ul v-if="errors.length > 0">
            <li v-for="(error, index) in errors" :key="index">{{error}}</li>
        </ul>
        <form action="#" class="space-y-6" @submit.prevent="createProject">
            <div>
                <label for="name">Name</label>
                <input type="text" v-model="name" id="name" class="px-2 py-2 w-full shadow rounded mt-2">
            </div>
            <div>
                <button type="submit" class="inline-block bg-blue-600 hover:bg-blue-700 text-white rounded px-4 py-2">Create Project</button>
                <span v-show="isLoading">Loading...</span>
            </div>
        </form>
    </div>
</template>

<script setup>

    const name = ref('');
    const errors = useState('errorsProjectCreate', () => []);
    const isLoading = ref(false);
    const router = useRouter();

    async function createProject(){
        isLoading.value = true;

        try {
            const resp = await useFetch(`http://localhost:8000/api/projects/`, {
                method: 'POST',
                body: {
                    name: name.value
                }
            });

            isLoading.value = false;
            name.value = '';
            router.push('/projects');

        } catch (e) {
            errors.value = Object.values(e.data.errors).flat();
            isLoading.value = false;
        }

    }

</script>

<style scoped>

</style>