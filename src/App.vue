<template>

<transition name="fade">
  <Modal @CloseModal="모달창열렸니 = $event" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니"/>
</transition>

  <div class="menu">
    <a v-for="(a, i) in 메뉴들" :key="i">{{ a }}</a>
  </div>

  <Discount v-if="showDiscount == true" :DiscountRatio="DiscountRatio" />

  <button @click="priceSort">가격낮은순정렬</button>
  <button @click="priceSortDesc">가격높은순정렬</button>
  <button @click="titleSort">상품명 가나다순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="a" v-for="(a, i) in 원룸들" :key="i" />


</template>

<script>
import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';



export default {
  name: 'App',
  data(){
    return {
      DiscountRatio: 30,
      showDiscount : true,
      원룸들오리지널 : [...data],
      오브젝트 : {name: 'kim', age: 20},
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수: [0, 0, 0],
      메뉴들: ['Home', 'Products', 'About'],
      products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
  methods : {
    increase(i){
      this.신고수[i] += 1;
    },

    priceSort(){
      this.원룸들.sort(function(a, b){
        return a.price - b.price
      })
    },

    priceSortDesc(){
      this.원룸들.sort(function(a, b){
        return b.price - a.price
      })
    },

    titleSort(){

      var a = ['안녕', '바보', '천재', '너는', '하하'];
      console.log(a.sort());
      this.원룸들.sort(function(a, b){
        return a.title - b.title
      })
    },


    sortBack(){
      this.원룸들 = [...this.원룸들오리지널];
    },
  },
  
  created(){
    // 서버에서 데이터 가져오는 코드
  },

  mounted(){
    setInterval(() => {
      if (this.DiscountRatio > 0){
        this.DiscountRatio--;
      }
    }, 1000)
  },

  // mounted(){
  //   setTimeout(()=>{
  //     this.showDiscount = false;
  //   }, 2000);
    
  // },

  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

body {
  margin: 0
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

.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(-1000px);
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to {
  opacity: 1;
  transform: translateY(0px);
}

.fade-leave-from {
  opacity: 1;
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to {
  opacity: 0;
}
</style>
