<template>
  <Navbar />

  <h1>영화정보</h1>
  <div v-for="(movie, i) in data" :key="i" class="item">
    <figure>
      <img :src="`${movie.imgUrl}`" :alt="movie.title">
    </figure>

    <div class="info">
      <h3 class="bg-yellow">{{ movie.title }}</h3>
      <p>개봉: {{ movie.year }}</p>
      <p>장르: {{ movie.category }}</p>
      <button @:click="increaseLike(i)">좋아요</button><span>{{ movie.like }}</span>

      <p>
        <button @click="isModal=true; selectedMovie=i; showValue(i)">상세보기</button>
      </p>
    </div>
  </div>

  <Modal />
</template>

<script>
  import data from './assets/movies'; // 영화 데이터
  import Navbar from './components/Navbar.vue';
  import Modal from './components/Modal.vue';
  
  export default {
    name: 'App', //컴포넌트명

    //문서에 표시될 변수 정의
    data(){
      return {//상태변수: 화면에 자주 업데이트 되는 내용들을 의미
        isModal: false,
        data : data,
        selectedMovie: 0,
      }
    },

    //내용이 길어질 경우, methods로 따로 빼서 함수 작성
    methods:{
      increaseLike(i){
        this.data[i].like += 1; //this를 작성해야 객체 안에 있는 like를 찾아서 함수를 실행함
      },
      showValue(val){
        console.log(`val === ${val}`);
      },
    },

    components: {
      Navbar: Navbar,
      Modal: Modal,
    }
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
