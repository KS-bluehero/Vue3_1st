<template>
  <div>
    <img :src="room.image" class="room-img">
    <h4 @click="$emit('openModal', room.id)"> {{room.title}} </h4>
    <!-- <h4 @click="ModalOpen = true; clickNo = i "> {{a.title}} </h4>
    <h5 @click="ModalOpen = true; clickNo = i "> {{a.content}} </h5>  -->
    <p> 월세 {{ comma(room.price)  }} 원 </p>
    <!-- <button @click="고발[i]++"> 허위매물신고 </button> <span>고발 건수 : {{고발[i]}}</span> -->
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    room : Object,
    clickNo : Number,
    ModalOpen : Boolean,

  },
  data(){
    return {
      comprice: 342345.10923,
    }
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