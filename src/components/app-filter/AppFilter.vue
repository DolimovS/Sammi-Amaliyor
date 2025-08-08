<template>
    <div class="btn-group" >
        <button v-for="title in filterBottons" :key="title.name" 
        class=" btn " type="button" 
        :class="[filterName==title.name?'btn-dark':'btn-outline-dark']"
        @click="filterHandler(title.name)"> {{ title.title }}</button>
    </div>
</template>

<script>
    export default {
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