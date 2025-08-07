<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form  @submit.prevent="addMovie" class="add-form d-flex" >
            <input 
            v-model="addName" 
            type="text" 
            class="form-control new-movie-label" 
            placeholder="Qanday kino">
             <input 
             v-model="addViewers" 
             type="number" 
             class="form-control new-movie-label" 
             placeholder="Necha marta ko'rilgan?">

             <button  class="btn btn-outline-dark" type="submit">Qo'shish</button>
        </form>
    </div>
</template>

<script>
    export default {
        data(){
           return{
             addName:'',
             addViewers:'',
           }
        },
        methods:{
            addMovie(){
                if(!this.name||!this.viewers)return
               const newMovie={
                name:this.addName,
                viewers:this.addViewers,
                favourite:false,
                like:false,
                id: Date.now()
            } 
            this.$emit('movieAdded',newMovie)
            console.log(newMovie);
            this.addName='';
            this.addViewers='';
            }
        }
    }
</script>

<style  scoped>
.movie-add-form{
        margin-bottom: 1rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>