<template>
    <div class="py-4 mt-3 mb-2 rounded-md px-4 bg-white shadow-sm hover:transition ease-in-out duration-500 hover:shadow-md cursor-pointer">
        <tr :class="disable === false ? '' : 'disabled line-through'" class="flex justify-around">
            <td>
                <input type="checkbox" name="disable" v-model="disable">
            </td>
            <td>{{ nom }}</td>
            <td>{{ prenom }}</td>
            <td>{{ poste }}</td>
            <td>{{ salaire }} €</td>
            <td>
                <span class="rounded-md text-xs" :class="disable === false ? 'bg-green-500 text-white text-center px-3 ':' bg-red-500 text-white text-center px-3'">
                   <span v-if="disable===false" class="lowercase">
                      Actif
                   </span>
                   <span v-else class="lowercase">
                      Inactif
                   </span>
                </span>
            </td>
            <td>
                <slot name="option">
                    <!--option...-->
                </slot>
            </td>
        </tr>

        <slot name="Edit">
              <!---Bloc Edit content-->
        </slot>
    </div>
</template>

<script>
export default {
    name: 'Tr',
    props: {
        nom: String,
        prenom: String,
        poste: String,
        salaire: Number,
        statut: String,
    },
    data() {
        return {
            disable: false,
        }
    }

}
</script>

<style scoped>
</style>