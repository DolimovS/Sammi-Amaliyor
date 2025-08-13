<template>
    <li class="list-group-item d-flex  justify-content-between  align-items-center "
        :class="[{ like: movie.like }, { favourite: movie.favourite }]">
        <p class="movie_count"><b>{{ index+1 }}</b></p>
        <span @click="$emit('onToggle', { id: movie.id, prop: 'like' })" class="list-group-item-label">{{ movie.name
            }}</span>
        <input type="number" class="list-group-item-input" :value="movie.viewers">

        <div class="d-flex justify-content-center align-items-center">
            <button class="btn-cookie btn-sm" type="button" @click="$emit('onToggle', { id: movie.id, prop: 'favourite' })">
                <i class="fas fa-cookie"></i>
            </button>

            <button @click="$emit('onRemove',movie.id)" class="btn-trash btn-sm" type="button">
                <i class="fas fa-trash"></i>
            </button>

            <i class="fas fa-star"></i>

        </div>
    </li>
</template>

<script>
export default {
    props: {
        movie: {
            type: Object,
            required: true
        },
        index:{
            type:Number,
            required:true,
        }
    },
    methods: {
        onLike(id) {
            this.$emit("onLike", id)
        }
    }
}


</script>

<style scoped>
.list-group-item {
    padding: 15px 20px;
    border: none;
    border-bottom: 1px solid #3d5a80;
}

.list-group-item:last-child {
    border: none;
}

.list-group-item span {
    line-height: 35px;
    font-size: 20px;
    cursor: pointer;
    width: 580px;
}

.list-group-item input {
    line-height: 35px;
    font-size: 20px;
    text-align: center;
    border: 0;
    outline: none;
}

.list-group-item button {
    width: 35px;
    height: 35px;

    margin: 3px;
    font-size: 17px;
    border: none;
    cursor: pointer;
}

.list-group-item .btn-cookie {
    color: #e09f3e;
}

.list-group-item .btn-trash {
    color: #e5383b;
}

.list-group-item .fa-star {
    width: 35px;
    height: 35px;
    text-align: center;
    line-height: 35px;
    font-style: 16px;
    color: #ffd700;
    transition: .3s all;
    transform: translate(30px);
    opacity: 0;
}

.list-group-item.like .fa-star {
    opacity: 1;
    transform: translateX(0);
}

.list-group-item.favourite .list-group-item-label,
.list-group-item.favourite .list-group-item-input {
    color: #e09f3e;
}
.movie_count {
    width: 20px;
    height: 30px;
    /* border: 1px solid red; */
    margin: 20px;
    display: flex;
    align-items: start;
    justify-content: center;
    
}

</style>