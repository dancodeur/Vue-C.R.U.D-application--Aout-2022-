<template>
    <div class="flex justify-center">
        <transition name="modal-search">
             <slot name="ModalContent">

             </slot>
        </transition>
    </div>
</template>

<script>
    export default {
        name:'ModalSearch',

    }
</script>

<style scoped>

.modal-search-enter-active{
   transition: ease-in-out 0.5s;
   transform: translateY(-5px);
}
.modal-search-leave-active{

    transition: ease-in-out 3s  cubic-bezier(0.075, 0.82, 0.165, 1);
    transform: translateY(-5px); 
}

.modal-search-enter-from,
.modal-search-leave-to{

    opacity: 0;
    transform: translateY(-45px);
}

</style>