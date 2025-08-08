<template>
    <div class="btn-group" >
        <PrimeryButton v-for="title in filterBottons" :key="title.name" 
        type="button" 
        :class="[filterName==title.name?'btn-dark':'btn-outline-dark']"
        @click="filterHandler(title.name)"> {{ title.title }}</PrimeryButton>
    </div>
</template>

<script>
import PrimeryButton from '../../ui-components/PrimeryButton.vue'
    export default {
        components:{
            PrimeryButton
        },
        props:{
            updateFilterHandler:{
                type:Function,
                required:true,
            },
            filterName:{
                type:String,
                required:true,
            }
        },
        data(){
            return{
                filter:'',
                filterBottons:[
                    {
                      title:'Barcha kinolar' ,
                      name:'all'  
                    },
                     {
                      title:'Mashhur  kinolar' ,
                      name:'popular'  
                    },
                     {
                      title:"Eng ko'p ko'rilgan  kinolar" ,
                      name:'mostWiewers'  
                    },
                ]
            }
        },
        methods:{
            filterHandler(filter){
                this.filter=filter
                this.updateFilterHandler(this.filter)
            }

        }
    }
</script>

<style  scoped>
 
</style>