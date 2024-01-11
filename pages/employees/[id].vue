<script setup>
const route = useRoute()

const { data: employee } = await useFetch('http://127.0.0.1:8000/api/v1/employees/' + route.params.id + '/')
</script>

<template>
    <div class="py-10 px-6 grid md:grid-cols-4 gap-3">
        <div class="md:col-span-3">
            <h1 class="mb-6 text-3xl">{{ employee.full_name }}</h1>
            <p>{{ employee.photo }}</p>
            <div class="space-x-4">
                <a v-bind:href="'/employees/delete/' + employee.id"
                    class="inline-block mt-6 py-4 px-6 bg-rose-700 text-white rounded-xl">Delete</a>
                <a v-bind:href="'/employees/update/' + employee.id"
                    class="inline-block mt-6 py-4 px-6 bg-teal-600 text-white rounded-xl">Update</a>
            </div>
        </div>

        <div class="md:col-span-1 p-6 bg-teal-700 text-white rounded-xl">
            <h3 class="mb-6 text-2xl">Supervisor</h3>

            <p class="mb-2">{{ employee.supervisor.full_name }}</p>
            
            <hr class="my-6 opacity-30">

            <h3 class="mb-6 text-2xl">Date offered</h3>

            <p>{{ employee.date_offered }}</p>
        </div>
    </div>
</template>