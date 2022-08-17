<template>
    <div class="bg-slate-50 px-8 py-3 text-sm text-slate-500">
        <Title title="Dashbord" />
        <slot name="content">
            Content here...
        </slot>
    </div>
</template>

<script>
import Title from '../components/Title.vue'; //Appel du composant Title...
    export default {
        name:'Dashbord',
        components:{
            Title,
        }

    }
</script>

<style scoped>

</style>