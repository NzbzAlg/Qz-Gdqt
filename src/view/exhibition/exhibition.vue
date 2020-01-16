<template>
  <div class="exhibition">
        <div class="content_left" style="margin-top:50px;" @click="twoZeroYear">
          <img src="../../assets/img/2020.png" alt="" style="width:100%;height:100%;cursor: pointer;">
        </div>
        <div class="content_middle" style="margin-top:50px;" @click="oneNineYear">
          <img src="../../assets/img/2019.png" alt="" style="width:100%;height:100%;cursor: pointer;">
        </div>
        <div class="content_right" style="margin-top:50px;" @click="oneEightYear">
          <img src="../../assets/img/2018.png" alt="" style="width:100%;height:100%;cursor: pointer;">
        </div>
  </div>
</template>
<script>
export default {
    data(){
      return{
        
      }
    },
    methods:{
      twoZeroYear(){
        this.$router.push('/index/twoZeroYear.vue')
      },
      oneNineYear(){
        this.$router.push('/index/oneNineYear.vue')
      },
      oneEightYear(){
        this.$router.push('/index/oneEightYear.vue')
      },
    }
}
</script>
<style lang='scss'>
  .exhibition{
    width: 100%;
    background: url(../../assets/img/背景图.jpg) no-repeat;
    background-size: 100% 100%;
    min-height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-around;
  }
</style>