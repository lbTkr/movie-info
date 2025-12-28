<template lang="">
    <div class="event" :class="{show : isOpen}">
        <p>{{ text }}</p>
        <button @click="isOpen=false">X</button>
    </div>
</template>
<script>
export default {
    name: 'EventComponent',
    //들어오는 값들을 여기서 관리함
    props: {
        text: String, // 들어오는 값 타입 명시
    },
    data(){
        return {
            isOpen: true,
        }
    }
}
</script>
<style>
    .event{display:none;background:#444;color:#fff;padding:10px 20px;text-align:center;font-size:small;}
    .event p{margin:0;}
    .event button{margin:0;}

    .show{display:flex;justify-content:space-between;}
</style>