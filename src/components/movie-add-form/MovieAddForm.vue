<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form @submit.prevent="addMovie" class="add-form d-flex">
            <Input v-model="addName" type="text" class=" new-movie-label" placeholder="Qanday kino"> </Input>
            <Input v-model="addViewers" type="number" class="new-movie-label" placeholder="Necha marta ko'rilgan?"> </Input>


            <PrimeryButton class=" btn-outline-dark" type="submit">Qo'shish</PrimeryButton>
        </form>
    </div>
</template>

<script>
import Input from '../../ui-components/Input.vue';
import PrimeryButton from '../../ui-components/PrimeryButton.vue'

export default {
    components: {
        PrimeryButton,
        Input,
    },
    data() {
        return {
            addName: '',
            addViewers: '',
        }
    },
    methods: {
        addMovie() {
            if (!this.addName || !this.addViewers) return;
            const newMovie = {
                name: this.addName,
                viewers: this.addViewers,
                favourite: false,
                like: false,
                id: Date.now()
            }
            this.$emit('movieAdded', newMovie)
            console.log(newMovie);
            this.addName = '';
            this.addViewers = '';
        }
    }
}
</script>

<style scoped>
.movie-add-form {
    margin-bottom: 1rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>