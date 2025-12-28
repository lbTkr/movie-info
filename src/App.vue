<template>
    <Navbar />
    <Event :text="text[eventTextNum]"/>

    <SearchBar :data="data_temp" @searchMovie="searchMovie($event)"/>

    <p><button @click="showAllMovie">전체보기</button></p>

    <Movies :data = "data_temp"
        @openModal="isModal=true; selectedMovie=$event"
        @increaseLike="increaseLike($event)"/>

    <Modal :data="data"
        :isModal="isModal"
        :selectedMovie="selectedMovie"
        @closeModal="isModal=false"/>
</template>

<script>
    import data from './assets/movies'; // 영화 데이터
    import Navbar from './components/Navbar.vue';                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  
    import Event from './components/Event.vue';
    import Movies from './components/Movies.vue';
    import Modal from './components/Modal.vue';
    import SearchBar from './components/SearchBar.vue';

    export default {
        name: 'App', //컴포넌트명

        //문서에 표시될 변수 정의
        data(){
            return {//상태변수: 화면에 자주 업데이트 되는 내용들을 의미
                isModal: false,
                data : data,
                data_temp : [...data], // 영화데이터 사본
                selectedMovie: 0,
                text: [
                    'NETPLIX 강렬한 운명의 드라마, 경기크리처',
                    '디즈니 100주년 기념작, 위시',
                    '그 날, 대한민국의 운명이 바뀌었다, 서울의 봄',
                ],
                eventTextNum: 0,
                interval: null,
            }
        },

        //내용이 길어질 경우, methods로 따로 빼서 함수 작성
        methods:{
            increaseLike(id){
                // this.data[i].like += 1; //this를 작성해야 객체 안에 있는 like를 찾아서 함수를 실행함
                this.data.find(movie => {
                    if(movie.id == id){
                        movie.like += 1;
                    }
                });
            },
            searchMovie(title){ // title: 검색어 키워드
                // 영화제목이 포함된 데이터를 가져옴
                this.data_temp = this.data.filter(movie => {
                    return movie.title.includes(title);
                });
            },
            showAllMovie(){
                this.data_temp = [...this.data];
            },
        },

        components: {
            Navbar: Navbar,
            Event: Event,
            Movies: Movies,
            Modal: Modal,
            SearchBar: SearchBar,
        },

        mounted(){
            this.interval = setInterval(() => {
                if(this.eventTextNum == this.text.length - 1){
                    this.eventTextNum = 0;
                }else{
                    this.eventTextNum += 1;
                }
            }, 3000);
        },
        unmounted(){
            clearInterval(this.interval); // 인터벌 해제
        },
    }
</script>

<style>
* {
    box-sizing: border-box;
    margin: 0;
}

body {
    max-width: 768px;
    margin: 0 auto;
    padding: 20px;
}

h1,
h2,
h3 {
    margin-bottom: 1rem;
}

p {
    margin-bottom: 0.5rem;
}

button {
    margin-right: 10px;
    margin-top: 1rem;
}

.item {
    width: 100%;
    border: 1px solid #ccc;
    display: flex;
    margin-bottom: 20px;
    padding: 1rem;
}

.item figure {
    width: 30%;
    margin-right: 1rem;
}

.item img {
    width: 100%;
}

.item .info {
    width: 100%;
}

.modal {
    background: rgba(0, 0, 0, 0.7);
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal .inner {
    background: #fff;
    width: 80%;
    padding: 20px;
    border-radius: 10px;
}
</style>
