<script setup>
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()

function logout() {
    userStore.removeToken()
}
</script>

<template>
    <div>
        <nav class="p-6 flex items-center justify-between bg-teal-800">
            <NuxtLink to="/" class="text-xl text-white">Employees Hierarchy</NuxtLink>
            <div class="flex items-center space-x-4">
                <NuxtLink to="/" class="text-white hover:text-teal-300">Home</NuxtLink>
            </div>
        </nav>
        <slot />
        <footer class="p-6 flex flex-wrap items-center justify-between bg-gray-900">
            <p class="text-gray-300">Copyright (c) 2023 - Employees Hierarchy</p>
            <div class="flex mt-6 md:mt-0 items-center space-x-4">
                <template v-if="userStore.user.isAuthenticated">
                    <NuxtLink to="/employees" class="py-4 px-6 bg-teal-900 hover:bg-teal-700 text-white rounded-xl">
                        Employees</NuxtLink>
                    <NuxtLink to="/employees/create" class="py-4 px-6 bg-teal-600 hover:bg-teal-700 text-white rounded-xl">
                        Create</NuxtLink>
                        <a v-on:click="logout" class="py-4 px-6 bg-rose-600 hover:bg-rose-700 text-white rounded-xl">Log out</a>
                </template>
                <template v-else>
                    <NuxtLink to="/login" class="py-4 px-6 bg-teal-900 hover:bg-teal-700 text-white rounded-xl">Log in
                    </NuxtLink>
                    <NuxtLink to="/signup" class="py-4 px-6 bg-teal-600 hover:bg-teal-700 text-white rounded-xl">Sign up
                    </NuxtLink>
                </template>
            </div>
        </footer>
    </div>
</template>
