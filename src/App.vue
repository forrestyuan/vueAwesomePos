<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <!-- <i class="icon iconfont icon-dianpu"></i>
    <i class="icon iconfont icon-hanbao"></i>
    <i class="icon iconfont icon-goumai"></i>
    <i class="icon iconfont icon-31huiyuanqia"></i>
    <i class="icon iconfont icon-shezhi"></i> -->
  
    <LeftNav/>
    <div class="main">
       <router-view/>  
      <Bottom/>
    </div>
  </div>
</template>

<script>
  import LeftNav from "@/components/common/LeftNav";
  import Bottom from "@/components/common/Bottom";
  export default {
    name: 'app',
    components:{
      LeftNav,
      Bottom
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow: auto;
}
.main{
  float: left;
  width: 95%;
  background-color: #eff2f7;

}
</style>
