<template>
  <div>
      <ul class="left-nav">
          <li>
              <i class="icon iconfont icon-goumai"></i>
              <div>收银</div>
          </li>
          <li>
              <i class="icon iconfont icon-dianpu"></i>
              <div>店铺</div>
          </li>
          <li>
              <i class="icon iconfont icon-hanbao"></i>
              <div>商品</div>
          </li>
          <li>
              <i class="icon iconfont icon-31huiyuanqia"></i>
              <div>会员</div>
          </li>
          <li>
              <i class="icon iconfont icon-zuanshi"></i>
              <div>统计</div>
          </li>
          <li>
              <i class="icon iconfont icon-shezhi"></i>
              <div>设置</div>
          </li>
      </ul>
  </div>
</template>
<script>
    export default{

    }
</script>
<style>
    .left-nav{
        color:#fff;
        font-size:10px;
        background-color:#20a0ff;
        float:left;
        width: 5%;
        /* min-width:40px; */
    }
    .iconfont{
        font-size: 24px;
    }
    .left-nav{
        padding: 0;
        margin: 0;
    }
    .left-nav li{
        list-style: none;
        text-align: center;
        border-bottom:1px solid #20a0ff;
        padding:10px;
    }
    .left-nav li:hover{
        color:#20a0ff;
        background-color: #fff;
        cursor: pointer;
    }
</style>
