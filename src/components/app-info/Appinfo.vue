<template>
    <div class="app-info">
        <p class="fs-3 text-uppercase">Barcha ko'rilganlar soni : {{ allMoviesCount }}</p>
        <p class="fs-4 text-uppercase">Ko'rilgan ko'rilganlar soni : {{ favouriteMoviesCount }}</p>
    </div>
</template>
 
<script>
export default {
    props:{
        allMoviesCount:{
            type:Number,
            required:true
        },
        favouriteMoviesCount:{
            type:Number,
            required:true
        }
    }
}
</script>

<style scoped>
.app-info {
    padding: 1.5rem ;
      background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>