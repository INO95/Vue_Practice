<template>

  <div class="black-bg" v-if="모달 == true">
    <div class="white-bg">
      <h4>상세페이지</h4>
      <p>상세페이지 내용</p>
      <button @click="모달 = false">닫기</button>
    </div>
  </div>

  <div class="menu">
    <!-- vue의 html 반복문 <태그 v-for="작명 in 몇회"> -->
    <!-- <a v-for="작명 in 3" :key="작명">home</a> -->
    <!-- vue 반복문의 특징 : array/object 집어넣기 가능 -->
    <!-- 자료안의 데이터 갯수만큼 반복되고 작명한 변수는 데이터안의 자료가 된다. forEach랑 비슷한듯? -->
    <!-- key의 용도 : 반복문으로 생성한 요소들을 구분하기 위한 속성 -->
    <!-- <a v-for="a in 메뉴들" :key="a">{{ a }}</a> -->
    <!-- 변수 작명은 2개까지 가능하며 왼쪽변수는 array 내의 데이터, 오른쪽 변수는 1씩 증가하는 정수 -->
    <a v-for="(a,i) in 메뉴들" :key="a">{{ i + 1 }} : {{ a }} </a>
    <!-- <a>products</a>
    <a>about</a> -->
  </div>

<!-- 밑 자료를 반복문으로 출력해보기 -->
  <div v-for="(a, i) in products" :key="a">
    <h4>{{products[i]}}</h4>
    <p>{{가격들[i]}} 만원</p>
  </div>

  <br><br><br><br><br>
  
  <div>
    <!-- 이러한 고정된 자료는 데이터 바인딩 할 필요가 없다 -->
    <!-- 원룸샵 -->
    <!-- HTML 속성도 데이터바인딩 할 수 있으며, {{ }} 이 아닌 :style 이런 식으로 사용 -->
    <!-- <h4 class="red" :style="스타일">XX 원룸</h4> -->
    <!-- 절대경로는 그냥 넣으면 되고 상대경로는 밑에처럼  -->
    <img :src="oneroom[0].image" class="room-img">
    <h4 @click="모달 = true">{{oneroom[0].title}}</h4>
    <!-- 데이터 바인딩 -> 중괄호 2개 -->
    <!-- <p>{{ price1 }} 만원</p> -->
    <p>{{oneroom[0].price}}</p>
    <!-- <button v-on:click="자바스크립트">허위매물신고</button> <span>신고수 : 0 </span> -->
    <!-- vue에서는 실시간 렌더링이 가능하기 때문에 변수만 변경해주면 html에는 자동으로 적용된다 -->
    <!-- <button @click="신고수++">허위매물신고</button> <span>신고수 : {{신고수}}</span> -->
    <!-- 함수를 만들어서 사용하는것도 가능하다. -->
    <button @click="increase(0)">허위매물신고</button> <span>신고수 : {{신고수[0]}}</span>
    <!-- <button @mouseover="신고수++">허위매물신고</button> <span>신고수 : {{신고수}}</span> -->
  </div>
  <div>
    <img :src="oneroom[1].image" class="room-img">
    <h4>{{oneroom[1].title}}</h4>
    <!-- <p>{{ price2 }} 만원</p> -->
    <p>{{oneroom[1].price}}</p>
    <button @click="increase(1)">허위매물신고</button> <span>신고수 : {{신고수[1]}}</span>
  </div>
  <div>    
    <img :src="oneroom[2].image" class="room-img">
    <h4>{{oneroom[2].title}}</h4>
    <!-- <p>{{ price2 }} 만원</p> -->
    <p>{{oneroom[2].price}}</p>
    <button @click="increase(2)">허위매물신고</button> <span>신고수 : {{신고수[2]}}</span>
  </div>
</template>

<script>

import data from './oneroom.js';
// 자바스크립트 스타일 데이터바인딩
// document.getElementById().innerHTML = ??

// 데이터바인딩을 하는 이유1 : HTML에 하드코딩해놓으면 나중에 변경이 어렵다.
// 데이터바인딩을 하는 이유2 : Vue의 실시간 자동 렌더링 기능
// -> vue에서는 data를 변경하면 data와 관련된 html도 변경된다. ( '{{ }}'' 사용시)
// 즉, 자주 변할거같은 데이터는 데이터로 보관하고 HTML에 {{꽂아넣는}} 방식으로 개발하라
export default {
  name: 'App',
  //데이터 보관함 (object 자료로 저장 {자료이름 : 자료내용})
  data(){
    return{
      //price1 : 60,
      //price2 : 70,
      //스타일 : 'color : blue',
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
      oneroom : data,
      메뉴들 : ['Home', 'Shop', 'About'],
      가격들 : ['50', '80', '40'],
      신고수 : [0,0,0],
      모달 : false,
    }
  },
  // 함수를 작성한다. 변수명 앞에는 this를 항상 붙여줘야 한다.
  methods : {
    increase(i){
      this.신고수[i] += 1;
    }
  },
  components: {
  }
}
</script>

<style>

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a{
  color: white;
  padding: 10px;
}
</style>
