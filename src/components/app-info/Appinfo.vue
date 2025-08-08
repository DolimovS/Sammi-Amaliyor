<template>
    <Box >
        <div>
            <p class="fs-3 text-uppercase">Barcha ko'rilganlar soni : {{ allMoviesCount }}</p>
            <p class="fs-4 text-uppercase">Ko'rilgan ko'rilganlar soni : {{ favouriteMoviesCount }}</p>
        </div>
    </Box>
</template>
 
<script>
    import Box from '../../ui-components/Box.vue';
export default {
    components:{
        Box
    },
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

</style>