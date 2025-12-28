<template lang="">
    <div v-for="(movie, i) in data" :key="i" class="item">
        <figure>
            <img :src="`${movie.imgUrl}`" :alt="movie.title">
        </figure>

        <div class="info">
            <h3 class="bg-yellow">{{ movie.title }}</h3>
            <p>개봉: {{ movie.year }}</p>
            <p>장르: {{ movie.category }}</p>
            <button @click="$emit('increaseLike', i)">좋아요</button><span>{{ movie.like }}</span>

            <p>
                <button @click="$emit('openModal', i)">상세보기</button>
            </p>
        </div>
    </div>
</template>
<script>
export default {
    name: 'MoviesComponent',
    props: {
        data: Array,
    },
    emits: ['openModal', 'increaseLike'],
}
</script>
<style lang="">
    
</style>