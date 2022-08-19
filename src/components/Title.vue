<template>
    <div class="mb-3 mt-3">
        <div class="flex justify-between">
            <h1 class="font-bold text-2xl text-slate-300">{{title}}</h1>
            <slot name="SVG">
                <!---SVG here...-->
            </slot>
        </div>
    </div>
</template>

<script>
    export default {
        name:'Title',
        props:{
            title:String,
        }
    }
</script>

<style scoped>

</style>