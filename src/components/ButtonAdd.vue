<template>
    <button @click="$emit('add')"
        class=" bg-green-600 dark:bg-blue-600 px-4 py-2 flex space-x-1 items-center hover:transition ease-in-out duration-500 hover:bg-green-500 dark:hover:bg-blue-500  active:transform active:scale-110">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 stroke-white " fill="none" viewBox="0 0 24 24"
            stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round"
                d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-2-5a4 4 0 11-8 0 4 4 0 018 0zM3 20a6 6 0 0112 0v1H3v-1z" />
        </svg>

        <span class="text-sm text-white">Add user </span>

    </button>
</template>

<script>
export default {
    name: 'ButtonAdd',
    emits:['add'],
}
</script>

<style scoped>
</style>