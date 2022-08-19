<template>
    <div class="dark">
         <div class="bg-slate-50 px-8 py-3 text-sm text-slate-500 dark:bg-black dark:text-slate-300">
        
            <Title title="Dashbord">
                <template #SVG>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 cursor-pointer" viewBox="0 0 20 20" fill="currentColor">
                            <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" />
                        </svg>
                </template>
            </Title>

            <slot name="content">
                <!--content here-->
            </slot>
        </div>
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