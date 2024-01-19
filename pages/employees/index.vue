<script setup>

const columns = [
    {
        key: 'id',
        label: 'ID',
        sortable: true
    },
    {
        key: 'full_name',
        label: 'Name',
        sortable: true
    },
    {
        key: 'photo',
        label: 'Photo'
    },
    {
        key: 'date_offered',
        label: 'Oferred',
        sortable: true
    },
    {
        key: 'job_title',
        label: 'Job position',
        sortable: true
    },
    {
        key: 'supervisor.full_name',
        label: 'Supervisor',
        sortable: true
    },
    {
        key: 'salary',
        label: 'Salary',
        sortable: true
    }
]

const hostname = useRuntimeConfig().public.url
// Fetching Data
const { data: employees } = await useFetch(hostname + `/api/v1/employees`)
const employeesArray = toRaw(employees.value)

// Selecting columns
const selectedColumns = ref([...columns])

// Filtering 
const q = ref('')

const filteredRows = computed(() => {
  if (!q.value) {
    return employeesArray
  }

  return employeesArray.filter((employee) => {
    return Object.values(employee).some((value) => {
      return String(value).toLowerCase().includes(q.value.toLowerCase())
    })
  })
})

// Paginating
const page = ref(1)
const pageCount = 10

const filteredAndPaginatedRows = computed(() => {
  return filteredRows.value.slice((page.value - 1) * pageCount, (page.value) * pageCount)
})

</script>

<template>
    <p>Employees List page</p>
    <div>
        <div class="flex px-3 py-3.5 border-b border-gray-200 dark:border-gray-700">
            <USelectMenu v-model="selectedColumns" :options="columns" multiple placeholder="Columns" />
        </div>
        <div class="flex px-3 py-3.5 border-b border-gray-200 dark:border-gray-700">
            <UInput v-model="q" placeholder="Filter employee..." />
        </div>

        <UTable :rows="filteredAndPaginatedRows" :columns="selectedColumns" />
        <div class="flex justify-end px-3 py-3.5 border-t border-gray-200 dark:border-gray-700">
            <UPagination v-model="page" :page-count="pageCount" :total="filteredRows.length" />
        </div>
    </div>
</template>