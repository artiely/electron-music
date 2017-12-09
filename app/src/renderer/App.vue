<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name: 'my-project'
  }
</script>

<style>
  /* CSS */
  body,html{
    min-width: 800px;
  }
  /*chrome滚动条*/
::-webkit-scrollbar-track-piece{
 -webkit-border-radius:0;
}
::-webkit-scrollbar{
 width:8px;
 height:8px;
}
::-webkit-scrollbar-thumb{
 height:50px;
 background-color:#000;
 -webkit-border-radius:4px;
 outline-offset:-2px;
 border: 2px solid #000;
}
::-webkit-scrollbar-thumb:hover{
 height:50px;
 background-color:#000;
 -webkit-border-radius:4px;
}
a{
  color: #fff
}
</style>
