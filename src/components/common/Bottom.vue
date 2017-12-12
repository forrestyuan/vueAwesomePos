<template>
  <div class="bottominfo">
      {{copyright}}
  </div>
</template>

<script>
  export default {
      data(){
          return{
              copyright:"copyright 2017"
          }
      }
  }
</script>

<style>
    .bottominfo{
        background-color: #ffffff;
        color: #222;
        height: 50px;
        width: 95%;
        padding: 20px;
    }
</style>
