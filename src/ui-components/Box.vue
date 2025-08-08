<template>
    <div class="box">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style  scoped>
.box{
    margin-bottom: 1rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>