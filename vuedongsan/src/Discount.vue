<template>
  <div class="discount">
    <p>지금사면 {{second}}% 할인</p>
  </div>
</template>

<script>
export default {
  name : 'discount',
  data(){
    return {
      second :30,
    }
  },
  mounted() {
    setInterval(() => {
      this.second--;
    }, 1000);
  }, 
   

}
</script>

<style>

</style>