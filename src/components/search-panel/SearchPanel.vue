<template>
    <div>
        <input  @input="changeHandler" :value="term"  type="text" class="form-control search-input" placeholder="Kinolarni qidirish">
    </div>
</template>

<script>

export default {
    data(){
        return{
            term:''
        }
    },
    props:{
        updateTermHandle:{
        type:Function,
        required:true
        }   
    },
    methods:{
        changeHandler(e){
            this.term=e.target.value
            this.updateTermHandle(this.term)
        }
    }



}
</script>

<style scoped>
.search-input {
    margin-bottom: 1rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>