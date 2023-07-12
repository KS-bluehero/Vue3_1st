<template>
  <div v-if="1 == 1">
    <h3 class="ks">Vue.js 공부하기 for KS</h3>
  </div>
  <div v-else>
    <h3 class="ks">Vue.js 공부하기 for HaHaHa</h3>
  </div>

  <div class="menu">
    <a v-for="(a,i) in menus" :key="i">{{a}}</a>    
  </div>

  <Discount v-if="showDiscount == true" />
 
  <button @click="SortBack">정렬초기화</button>
  <button @click="priceSort">가격순정렬</button>
  <button @click="priceSortReverse">가격역순정렬</button>
  <button @click="ABCSort">명칭순정렬</button>


  <transition name="fade">
    <Modal @close="ModalOpen = false" :rooms="rooms"  :clickNo="clickNo"  :ModalOpen="ModalOpen" />    
  </transition>


  <Card @openModal="ModalOpen = true; clickNo=  $event" :room="rooms[i]" :clickNo="clickNo"  :ModalOpen="ModalOpen" v-for="(a,i) in rooms" :key="a" />

<!--   
  <div v-for="(a,i) in rooms" :key="i">
    <img :src="a.image" class="room-img">
    <h4 @click="ModalOpen = true; clickNo = i "> {{a.title}} </h4>
    <h5 @click="ModalOpen = true; clickNo = i "> {{a.content}} </h5> 
    <p> 월세 {{ a.price  }} 원 </p>
    <button @click="고발[i]++"> 허위매물신고 </button> <span>고발 건수 : {{고발[i]}}</span>
  </div> -->

  <!-- <div v-for="(a,i) in 원룸들" :key="i">
    <img :src="원룸들[i].image" class="room-img">
    <h4 @click="ModalOpen = true; clickNo = i "> {{원룸들[i].title}} </h4>
    <h5> {{원룸들[i].content}} </h5>
    <p> 월세 {{ 원룸들[i].price  }} 원 </p>
    <button @click="고발[i]++"> 허위매물신고 </button> <span>고발 건수 : {{고발[i]}}</span>
  </div> -->
  
  <!-- <div v-for="(a,i) in products" :key="i">    
    <img src="./assets/room0.jpg"  class="room-img">
    <h4 @click="ModalOpen = true"> {{a}} </h4>
    <p> 월세 {{price[i]}} 만원 </p>  
    <button @click= "고발[i]++"> 허위매물신고 </button> 
    <span>고발 건수 : {{고발[i]}}</span>
  </div>   -->
  
  <!-- <div>
    <img src="./assets/room1.jpg" class="room-img">
    <h4> {{products[1]}} </h4>
    <p> 월세 {{price[1]}} 만원 </p>
    <button v-on:Click="신고수[1]++">허위매물신고</button> <span>신고 Count : {{신고수[1]}}</span>
  </div>

  <div>
    <img src="./assets/room2.jpg" class="room-img">
    <h4> {{products[2]}} </h4>
    <p> 월세 {{price[2]}} 만원 </p>
    <button @Click="신고수[2]++">허위매물신고</button> <span>신고 Count : {{신고수[2]}}</span>
  </div> -->
</template>

<script>
import oneroom from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';
export default {
  name: 'App',
  data(){
    return {
      showDiscount : true,
      original : [...oneroom],
      clickNo : 0,
      rooms : oneroom,
      ModalOpen : false, 
      고발 : [0,0,0,0,0,0],
      스타일 : 'color:blue',
      menus : ['Home', 'Products','About'],
      price : [80,90,100],
      products : ["역삼동원룸", '천호동원룸', '마포구원룸'],
    }
  },
  methods: {
    increase(){
      this.고발++ ;
    },
    SortBack(){
      this.rooms = [...this.original];
    },
    priceSort(){
      this.rooms.sort(function(a,b){
        return a.price-b.price;
      })
    },
    priceSortReverse(){
      this.rooms.sort(function(a,b){
        return b.price-a.price;
      })
    },
    ABCSort(){
      this.rooms.sort(function(a,b){
        let x = a.title.toLowerCase();
        let y = b.title.toLowerCase();
        if(x<y){
          return -1;
        }else if(x>y){
          return 1;
        } return 0;
      });
    }       
  },
  mounted(){
    setTimeout(() => {
      this.showDiscount = false;
    }, 3000);

  },
  components: {
    Discount: Discount,
    Modal: Modal,
    Card: Card,                //좌우 동일 명칭으로 하면 하나로 처리 가능
  }                        
}
</script>

<style>
body {
  margin : 0
 }
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; 
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.discount {
  background: #eee;
  padding: 10px;
  margin: 5px;
  border-radius: 10px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 1px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color : white;
  padding: 10px;
}

.room-img {
  width: 50%;
  margin-top: 40px;
}

h3 {
  color : rgb(200, 20, 47);
  text-align: center;
  font-style: italic;
}

.fade-enter-from {
  opacity: 0;
  transform: translate(-1000px);
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
