<template>
    <div class="px-8 py-4 mt-8">
        <div class="flex space-x-4 justify-end items-center mb-5">

           <slot name="Button">
                <!--Button...-->
           </slot>
        
        </div>

        <!--Bloc de Modal de recherche ici et de modification -->

        <div>
            <slot name="AS">
                  <!--Add and Search...-->    
            </slot> 
        </div>


        <table class="w-full py-3 px-4 text-sm">
            <thead>
                <div class="flex ">
                    <tr v-for="Th in th" :key="Th.title" class="w-full">
                        <Th :title="Th.title" />
                    </tr>
                </div>
            </thead>

            <tbody>
                <div>
                    <slot name="tbody">
                        <!--content of tody-->
                    </slot>
                </div>
            </tbody>
        </table>
    </div>
</template>

<script>
import Th from './Th.vue';
export default {
    name: 'Tab',
    components: {
        Th,
    },
    data() {

        return {
            th: [
                { title: 'Statut' },
                { title: 'Nom' },
                { title: 'Prénom' },
                { title: 'Poste' },
                { title: 'Salaire' },
                { title: 'Etat' },
                { title: 'Option' }

            ],
        }
    },

}
</script>

<style scoped>
</style>