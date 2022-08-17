<template>
  <Dashbord>
    <template #content>
     
     <ModalSearch>
          <template #ModalContent>
              <div v-if="ModalSearch" class="bg-white shadow-md absolute w-[50%] h-[20%] px-4 py-4 text-slate-400 text-sm rounded-sm">
                 <!--search icon-->
                 <div class="flex justify-end">
                      <svg @click="closeSearch()" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 cursor-pointer hover:transition ease-linear duration-300 hover:stroke-red-500 active:transform active:scale-110 " fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                      </svg>
                 </div>
                 
                 <!--search Modal search input-->
                 <div class="px-4 flex mt-2 items-center group space-x-1 border-b-2  border-spacing-2">
                     <div>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 group-hover:stroke-green-500" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                              <path stroke-linecap="round" stroke-linejoin="round" d="M8 16l2.879-2.879m0 0a3 3 0 104.243-4.242 3 3 0 00-4.243 4.242zM21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                        </svg>
                     </div>
                     <input type="text" placeholder="search user..." v-model="UserSearch" class="px-3 py-2 outline-none w-full focus:text-green-500 " >
                 </div>
                <!--Botton bloc (vous recherchez...)-->
                 <div class="mt-2 flex justify-center">
                      <p v-if="UserSearch != ''">Vous recherchez : <span class="lowercase font-semibold">{{UserSearch}}</span></p>
                 </div>


              </div>
          </template>
      </ModalSearch>

      <Tab>
        <!--Begin Button-->
         <template #Button>
          
              <ButtonSearch @search="toggleSearch()" />
              <ButtonAdd @add="add()" />

         </template>
         <!----Fin-->

         <template #AS>
             <transition name="add">
                   <div class="bg-white rounded-md text-sm px-4 py-4 mb-3"  v-if="blocAdd">
                       <div class="flex justify-around items-center">
                            <input type="text" placeholder="Nom" v-model="nom" class="px-3 py-2 outline-none rounded-md bg-slate-50 place-content-center placeholder-slate-300 text-sm focus:transition ease-in-out duration-300 focus:bg-transparent focus:outline-slate-100 focus:rounded-none focus:outline-1 focus:placeholder-slate-300">
                            <input type="text" placeholder="Prénom" v-model="prenom" class="px-3 py-2 outline-none rounded-md bg-slate-50 place-content-center placeholder-slate-300 text-sm focus:transition ease-in-out duration-300 focus:bg-transparent focus:outline-slate-100 focus:rounded-none focus:outline-1 focus:placeholder-slate-300">
                            <input type="text" placeholder="Poste" v-model="poste" class="px-3 py-2 outline-none rounded-md bg-slate-50 place-content-center placeholder-slate-300 text-sm focus:transition ease-in-out duration-300 focus:bg-transparent focus:outline-slate-100 focus:rounded-none focus:outline-1 focus:placeholder-slate-300">
                            <input type="number" placeholder="Salaire" v-model="salaire" class="px-3 py-2 outline-none rounded-md bg-slate-50 place-content-center placeholder-slate-300 text-sm focus:transition ease-in-out duration-300 focus:bg-transparent focus:outline-slate-100 focus:rounded-none focus:outline-1 focus:placeholder-slate-300">
                            <button @click="save()" class=" bg-green-600 px-4 text-white py-2 flex space-x-1 items-center hover:transition ease-in-out duration-500 hover:bg-green-500 active:transform active:scale-110">
                               Confirmé
                            </button>
                            <div>
                                <svg @click="close()" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 cursor-pointer hover:transition ease-linear duration-300 hover:stroke-red-500 active:transform active:scale-110 " fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                                </svg>
                            </div>
                       </div>
                   </div>
             </transition>

         </template>


        <template #tbody>
          <div v-for="persons in SearchFilter" :key="persons.id" class="w-full relative">
              <!--props du composant perosn...-->
              <Tr :nom="persons.nom" :prenom="persons.prenom" :poste="persons.poste" :salaire="persons.salaire" :statut="persons.statut">
                  <template #option>
                      <svg @click="OptionModal(persons.id)" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                           <path stroke-linecap="round" stroke-linejoin="round" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z" />
                      </svg>

                      <!--Modal Option-->
                      <div v-show="ModalOption" :class="persons.id === ModalId ?'':'hidden'" class="bg-white text-slate-500 text-sm px-6 py-3 shadow-md rounded-md absolute -top-16  -right-6">
                          <div @click="Edit(persons.id)" class="flex space-x-2 items-center mb-2 group focus:animate-ping">
                              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 group-hover:stroke-red-500 hover:transition duration-300 ease-in-out hover:transform hover:scale-125 group-active:animate-ping " fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                   <path stroke-linecap="round" stroke-linejoin="round" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                              </svg>
                             <span class="text-slate-500 text-sm group-hover:text-red-500 group-active:animate-ping">Edit</span>
                          </div>
                          <!--Bloc 2...-->
                          <div @click=Delete(persons.id) class="flex space-x-2 items-center mb-2 group">
                              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 group-hover:stroke-red-500 hover:transition duration-300 ease-in-out hover:transform hover:scale-125 group-active:animate-ping " fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                  <path stroke-linecap="round" stroke-linejoin="round" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                              </svg>
                             <span class="text-slate-500 text-sm group-hover:text-red-500 group-active:animate-ping">Delete</span>
                          </div>
                      </div>
                      <!--Fin du Modal option...-->
                  </template>

              </Tr>
              <!--Edit Bloc...-->
              <div>
                   <transition name="edit">
                      <div class="bg-white rounded-md shadow-sm text-sm px-4 py-3 mb-3"  v-show="blocEdit" :class="persons.id === EditId?'':'hidden'">
                          <div class="flex justify-around items-center">
                               <input type="text"  placeholder="Nom" v-model="persons.nom" class="px-3 py-2 outline-none rounded-md bg-slate-50 place-content-center placeholder-slate-300 text-sm focus:transition ease-in-out duration-300 focus:bg-transparent focus:outline-slate-100 focus:rounded-none focus:outline-1 focus:placeholder-slate-300">
                               <input type="text"  placeholder="Prénom" v-model="persons.prenom" class="px-3 py-2 outline-none rounded-md bg-slate-50 place-content-center placeholder-slate-300 text-sm focus:transition ease-in-out duration-300 focus:bg-transparent focus:outline-slate-100 focus:rounded-none focus:outline-1 focus:placeholder-slate-300">
                               <input type="text"  placeholder="Poste" v-model="persons.poste" class="px-3 py-2 outline-none rounded-md bg-slate-50 place-content-center placeholder-slate-300 text-sm focus:transition ease-in-out duration-300 focus:bg-transparent focus:outline-slate-100 focus:rounded-none focus:outline-1 focus:placeholder-slate-300">
                               <input type="number" placeholder="Salaire" v-model="persons.salaire" class="px-3 py-2 outline-none rounded-md bg-slate-50 place-content-center placeholder-slate-300 text-sm focus:transition ease-in-out duration-300 focus:bg-transparent focus:outline-slate-100 focus:rounded-none focus:outline-1 focus:placeholder-slate-300">
                               <div>
                                   <svg @click="closeEdit()" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 cursor-pointer hover:transition ease-linear duration-300 hover:stroke-red-500 active:transform active:scale-110 " fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                       <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                                   </svg>
                               </div>
                          </div>
                      </div>
                  </transition>
              </div>



          </div>
        </template>

      </Tab>
    </template>
  </Dashbord>
</template>

<script>

let id=0;

import Dashbord from './Template/Dashbord.vue';
import Tab from './components/Tab.vue';
import Tr from './components/Tr.vue';
import ButtonAdd from './components/ButtonAdd.vue';
import ButtonSearch from './components/ButtonSearch.vue';
import ModalSearch from './components/ModalSearch.vue';


export default {

  components: {
    Dashbord,
    Tab,
    Tr,
    ButtonAdd,
    ButtonSearch,
    ButtonAdd,
    ModalSearch,
},
  data() {
      return {
        person:[
          { id:id++,nom:'Elenga',prenom:'Dan David',poste:'Développeur Web',salaire:6000},
          { id:id++,nom:'Elenga',prenom:'Dan David',poste:'Développeur Web',salaire:6000},
        ],
        
        //Data pour user...
        nom:'',
        prenom:'',
        poste:'',
        salaire:'',
      

        //Fin des data pour user...

        ModalOption:false,
        ModalId:'',
        blocAdd:false,
     
        //Search modal...
        UserSearch:'',
        ModalSearch:false,

        //Edit option
        blocEdit:false,
        EditId:'',
      }
  },

  methods:{

    OptionModal(id){

       this.ModalId=id;

       if(this.ModalOption==false){
           this.ModalOption=true;
       }else{
           this.ModalOption=false;
       }
    },

    save(){
        
        if(this.nom !=''){
          if(this.prenom !=''){
            if(this.poste !=''){
              if(this.salaire !=''){

                this.person.push({id:id++,nom:this.nom,prenom:this.prenom,poste:this.poste,salaire:this.salaire}); //Les infos sont sauvegardé dans la DataBase
                this.nom='';
                this.prenom='';
                this.poste='';
                this.salaire='';
              
              }
            }
          }
        }
    
    },

    add(){

      if(this.blocAdd==false){
         this.blocAdd=true;
         this.ModalSearch=false;

      }else{
        this.blocAdd=false;
      }

    },

    close(){

      this.blocAdd=false;
    },

    toggleSearch(){

      if(this.ModalSearch==false){
         this.ModalSearch=true;
         this.blocAdd=false;
      }else{
         this.ModalSearch=false;
      }
    },

    closeSearch(){
      this.ModalSearch=false;
    },

    Edit(id){
      
      this.EditId=id; 

      if(this.blocEdit==false){
        this.blocEdit=true;
      }else{
        this.blocEdit=false;
      }
    },

    closeEdit(){
      this.blocEdit=false;

    },

    Delete(id){

      this.person=this.person.filter(persons=>persons.id !== id); //delete element from database in vue.js
    }



    
  },

//Computed... search méthode...

  computed:{

    SearchFilter(){

      return this.person.filter(persons=>persons.nom.toLocaleLowerCase().includes(this.UserSearch.toLocaleLowerCase()));
    }
  }
}
</script>

<style scoped>

/****Modal Search transition */
.add-enter-active,
.add-leave-active{

  transition: opacity ease-in-out 0.3s ;
}
.add-enter-from,
.add-leave-to{
  opacity:0;
  transform: scaleY(20px);
}
/****Edit transition */
.edit-enter-active,
.edit-leave-active{

  transition: ease-in-out 0.5ms;
  transform: translateY(25px);
}

.edit-enter-from,
.edit-leave-to{

  opacity: 0;
  transform: translateY(-25px);
}
</style>
