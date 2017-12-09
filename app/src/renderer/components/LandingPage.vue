<template>
  <div id="wrapper">
    <div class="top-nav">
      <div class="logo">
        <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--snowflake"></use>
          </svg>
      </div>
      <div class="search">
        <div class="searc-bar">
          <input type="text"> <i class="iconfont icon-search"></i>
        </div>
      </div>
      <div class="tools">
        <span class="tool-icon min"><i class="iconfont icon-zuixiaohua"></i></span>
        <span class="tool-icon max"><i class="iconfont icon-zuidahua"></i></span>
        <span class="tool-icon close"><i class="iconfont icon-guanbi"></i></span>
      </div>
    </div>
    <div class="left-menu">
      <ul>
        <li class="menu-title">推荐</li>
        <li class="menu-item active">
          <router-link to="index" tag="div">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--snowman"></use>
          </svg>
          发现音乐
          </router-link>
        </li>
        <li class="menu-item">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--bird"></use>
          </svg>
          死人FM</li>
        <li class="menu-item">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--toast"></use>
          </svg>MV</li>
        <li class="menu-item">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--cone"></use>
          </svg>朋友</li>
      </ul>
      <ul>
        <li class="menu-title">我的音乐</li>
        <li class="menu-item">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--snowman"></use>
          </svg>
          本地音乐
        </li>
        <li class="menu-item">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--bird"></use>
          </svg>
          我的歌手</li>
        <li class="menu-item">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--toast"></use>
          </svg>我的云盘</li>
        <li class="menu-item">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon--cone"></use>
          </svg>我的MV</li>
      </ul>
    </div>
    <div class="router-view">
      <router-view></router-view>
    </div>
    <div class="player">
      <table>
        <tr>
          <td style="padding-left:20px"><i class="iconfont icon-prev1"></i></td>
          <td style="padding:0 10px"><i class="iconfont icon-bofang" style="font-size:35px"></i></td>
          <td style="padding-right:20px"><i class="iconfont icon-prev"></i></td>
          <td style="width:476px"><div class="p-box">0:25<div class="progress-bar"><div class="bar"></div></div>3:52</div></td>
          <td style="width:130px"><div><i class="iconfont icon-yinliang1"></i><div class="vol-bar"><div class="bar"></div></div></div></td>
          <td><i class="iconfont icon-renwu_xh" style="font-size:24px"></i></td>
          <td></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
  import SystemInformation from './LandingPage/SystemInformation'
  import $ from 'jquery'
  var ipcRenderer = require('electron').ipcRenderer
  var isBig = true // 窗口放大还原标示

  export default {
    name: 'landing-page',
    components: { SystemInformation },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
      }
    },
    mounted () {
      // 关闭窗口
      $(document).on('click', '.close', function () {
        console.log(1)
        ipcRenderer.send('hide-main-window')
      })
      // 最大化
      $(document).on('click', '.max', function () {
        if (isBig) {
          ipcRenderer.send('show-window')
        } else {
          ipcRenderer.send('orignal-window')
        }
        isBig = !isBig
      })
      // 最小化
      $(document).on('click', '.min', function () {
        ipcRenderer.send('hide-window')
      })
    }
  }
</script >

<style lang="less">
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  #wrapper{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  .icon {
    width: 1em;
    height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
    margin-right: 4px;
  }
  body {
    font-family: 'Source Sans Pro', sans-serif;
  }
  .top-nav {
    background: #222222;
    position: fixed;
    -webkit-user-select: none;
    -webkit-app-region: drag;
    top: 0;
    left: 0;
    right: 0;
    height:48px;
    z-index: 99;
    .logo {
      width: 48px;
      height: 48px;
      float: left;
      // background: #000;
      // background: url(../assets/logo.png) no-repeat 0 0;
      // background-size: 100%
      .icon{
        width: 48px;
        height: 48px;
        padding: 8px
      }
    }
    .tools{
      -webkit-app-region:no-drag;
      float: right;
      color: #777;
      .tool-icon{
        padding: 8px;
        cursor: pointer;
        &:hover{
          color: #fff;
        }
      }
    }
  }
  .left-menu {
    width: 200px;
    height: 100%;
    background: #191b1f;
    position: absolute;
    top: 48px;
    left: 0;
    .menu-title {
      height: 30px;
      line-height: 30px;
      font-size: 14px;
      color: #777;
      padding-left: 10px;
    }
    .menu-item {
      font-size: 14px;
      height: 30px;
      line-height: 30px;
      padding-left: 15px;
      border-left: 4px solid transparent;
      color: #eeeeee;
      cursor: pointer;
      &:hover {
        color: #fff
      }
      &.active{
        background: #222;
        border-color: #bb1616
      }
    }
  }
  .router-view{
      background: #16181c;
      position: absolute;
      left: 200px;
      top: 48px;
      bottom: 0;right: 0;
      overflow-y: scroll;
      padding-bottom: 100px
    }
  .player{
    height: 48px;
    position: absolute;
    z-index: 99;
    left: 0;
    right: 0;
    bottom: 0;background: #222;
    .p-box{
      color: #999;
      font-size: 12px;
    }
    table{
      width: 100%;
      height: 100%;
      i{
        font-size: 28px;
        color: #777;
      }
      .icon-yinliang1{
        font-size: 18px;
      }
      .progress-bar{
        position: relative;
        display: inline-block;
        width: 400px;
        height: 4px;
        border-radius: 4px;
        background: #333;
        margin: 2px 10px;
        overflow: hidden;
        .bar{
          position: absolute;
          top: 0;
          left: 0;
          background: #bb1616;
          height: 100%;
          width: 20%;
        }
      }
      .vol-bar{
        height: 3px;
        width: 100px;
        background: #333;
        border-radius: 3px;
        display: inline-block;
        vertical-align: middle;
        margin-left: 8px;
        position: relative;
        top: -3px;
        overflow: hidden;
        .bar{
          height: 100%;
          position: absolute;
          top: 0;
          left: 0;
          width: 80%;
          background: #bb1616;
        }
      }
    }
  }
  .search{
    position: relative;
    float: left;
    padding: 12px 0 0 60px;
    .searc-bar{
      position: relative;
      height: 22px;
      width: 180px;
      border-radius: 12px;
      background: #111;
      input{
        text-indent: 14px;
        background: transparent;
        outline: none;
        border: none;
      }
      .iconfont{
        position: absolute;
        top: 3px;
        right: 5px;
        color: #999;
        cursor: pointer;
      }
    }
  }
  
</style>
