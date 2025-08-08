<template>
    <div class="btn-group">
        <button 
        class=" btn " type="button" 
        :class="[filterName=='all'?'btn-dark':'btn-outline-dark']"
        @click="filterHandler('all')">Barcha kinolar
    </button>
        <button 
        class=" btn btn-outline-dark" type="button" 
        :class="[filterName=='popular'?'btn-dark':'btn-outline-dark']"
        @click="filterHandler('popular')">Mashhur  kinolar
    </button>
        <button 
        class=" btn btn-outline-dark" type="button" 
        :class="[filterName=='mostWiewers'?'btn-dark':'btn-outline-dark']"
        @click="filterHandler('mostWiewers')">Eng ko'p ko'rilgan  kinolar
    </button>
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
                filter:''
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