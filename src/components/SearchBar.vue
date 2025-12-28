<template lang="">
    <div class="search-box">
        <input 
            type="search"
            @change="inputText = $event.target.value"
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
    },
    // 검사할 항목 추가
    /*
     *  watch: {} 안에 있는 함수명은 검사할 변수명(data() 안의 'inputText')과 동일하게 작성하면 되고
        작성 규칙은 다음과 같다

        검사할 변수명(변경값, 이전값(도 확인 가능)){
            로직
        }
        
        inputText가 바뀔 때마다 name에 값이 들어감
     */
    watch: { // watch는 보통 Hook이라고 하는데 사용자가 사용하면 감시하고 중간에 채가는 형태
        inputText(name){
            if(name !== "액시트"){// 입력한 영화제목이 데이터에 있는지 확인
                alert('해당하는 영화가 없습니다');
            }
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