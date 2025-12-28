<template lang="">
    <div class="search-box">
        <input 
            type="search"
            v-model="inputText"
            placeholder="검색어 입력"
        >
        <!-- v-model => 사용자에게 받은 값을 변수에 자동으로 저장해줌 -->
        <button>검색</button>
    </div>
    <p>{{ inputText }}</p>
</template>
<script>
export default {
    name: "SearchBarComponent",
    data(){
        return {
            inputText: "",
        }
    }
}
</script>
<style>
.search-box{
    padding:10px;
    display:flex;
    justify-content:center;
}
.search-box input{
    padding:5px 10px;
}
.search-box button{
    margin:0;
}
</style>