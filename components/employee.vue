<script setup>
import { useUserStore } from '@/stores/user';

const userStore = useUserStore()

const emit = defineEmits(['deleteEmployee'])

const props = defineProps({
    my: {
        type: [Boolean]
    },
    employee: {
        type: [Object]
    }
})

async function deleteEmployee(id) {
    await $fetch('http://127.0.0.1:8000/api/v1/employees/' + id + '/delete/', {
        method: 'DELETE',
        headers: {
            'Authorization': 'token ' + useUserStore.user.token,
            'Content-Type': 'application/json'
        },
    })
    .then(response => {
        console.log('response', response)

        emit('deleteEmployee', id)
    })
    .catch(error => {
        console.log(error)
    })
}
</script>

<template>
    <div class="p-6 flex items-center justify-between bg-gray-100 rounded-xl">
        <div>
            <h3 class="mb-2 text-xl font-semibold">{{ employee.full_name }}</h3>
            <p class="text-gray-600">{{ employee.supervisor.full_name }}</p>
        </div>

        <div>
            <p class="mb-2">{{ employee.job_title }}</p>
            <p>{{ employee.salary }}</p>
        </div>

        <div>
            <p>Offered {{ employee.date_offered }}</p>
        </div>

        <div class="space-x-4">
            <NuxtLink v-bind:to="'/employees/' + employee.id" class="py-4 px-6 bg-teal-700 text-white rounded-xl">Detail</NuxtLink>
            <NuxtLink v-bind:to="'employees/' + employee.id + '/update/'" class="py-4 px-6 bg-cyan-700 text-white rounded-xl" v-if="my">Update</NuxtLink>
            <a @click="deleteEmployee(employee.id)" class="py-4 px-6 bg-rose-700 text-white rounded-xl" v-if="my">Delete</a>
        </div>
    </div>
</template>