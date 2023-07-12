<template>
  <div class="black-bg" v-if="ModalOpen == true">
    <div class="white-bg">
      <img :src="rooms[clickNo].image" class="room-img">
      <h4>{{rooms[clickNo].title}}</h4>
      <p>{{rooms[clickNo].content }}</p>
      <strong style="font-family: 'Courier New', Courier, monospace; font-size: 14px;">월단위 입력란 </strong>
      <input v-model="month">
      <input type="range" min="1" max="12">
      <!-- <input @input="month = $event.target.value"> -->
      <p> {{month}}개월 선택함 : {{ comma(rooms[clickNo].price *month) }} 원 </p>
      <button @click="$emit('close')"> 닫기 </button>      
    </div>
  </div>
</template>

<script>

export default {
  name: 'Modal',
  props: {
    rooms : Array,
    clickNo : Number,
    ModalOpen : Boolean,
  },
  data() {
    return {
      month : null,
    }
  },
  watch: {
    month(a){
      if(a>12){
        alert('13개월 이상 입력 불가')
        this.month = 1;        
      } else if(isNaN(a)){
        alert('문자 입력 불가')
        this.month = 1;      
      }
    }
  },
  beforeUpdate(){
      if(this.month == 2 || this.month == 1){
        alert('3개월부터 12개월중으로 입력하세요')
        this.month = 3;
      }
  },

  components: {

  },
  methods: {
    comma(val) {        
        return val.toFixed(0).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },

}
</script>

<style>

</style>