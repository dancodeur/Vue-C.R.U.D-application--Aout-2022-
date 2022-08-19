<template>
    <div :class="dark?'':'dark'">
         <div class="bg-slate-50 px-8 py-3 text-sm text-slate-500 dark:bg-black dark:text-slate-300">
        
            <Title title="Dashbord">
                <template #SVG>
                    <div>
                        <svg v-if="dark==true" @click="Dark()" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 fill-purple-500 cursor-pointer" viewBox="0 0 20 20" fill="currentColor">
                            <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" />
                        </svg>
                        <svg v-else @click="Dark()" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 cursor-pointer fill-yellow-500" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z" clip-rule="evenodd" />
                        </svg>
                    </div>
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
         },

         data(){

            return {
                dark:true,
            }
         },

         methods:{

            Dark(){
                

                if(this.dark==false){
                    this.dark=true;
                }else{
                    this.dark=false;
                }
            }

         },

         computed:{
            //Computed...
         }


    }
</script>

<style scoped>

</style>