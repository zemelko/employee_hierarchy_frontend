<script setup>
const { data: employees } = await useFetch('http://127.0.0.1:8000/api/v1/employees/')
</script>

<template>
    <p>Employees List page</p>
    <Employee
    v-for="employee in employees.results" 
    v-bind:key="employee.id"
    v-bind:employee="employee"
    />
</template>