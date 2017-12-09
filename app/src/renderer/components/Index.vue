<template>
  <div>
    <!-- swiper -->
    <swiper :options="swiperOption" class="banner">
      <swiper-slide><img src="../../../static/banner/1.jpg" alt=""></swiper-slide>
      <swiper-slide><img src="../../../static/banner/2.jpg" alt=""></swiper-slide>
      <swiper-slide><img src="../../../static/banner/3.jpg" alt=""></swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
      <div class="swiper-button-prev" slot="button-prev"></div>
      <div class="swiper-button-next" slot="button-next"></div>
    </swiper>
    <div class="newsongs">
      <div v-for="(item,index) in songs" :key="index">
        <div class="songs-list">
          <div class="item">
            <div class="des-box">
              <p class="des">{{item.description}}</p>
            </div>
          <p class="count"><i class="iconfont icon-erji"></i>{{item.subscribedCount}}</p>
          <img :src="item.coverImgUrl" alt="">
          <p class="title">{{item.name}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data () {
      return {
        swiperOption: {
          pagination: {
            el: '.swiper-pagination',
            type: 'progressbar'
          },
          navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev'
          },
          loop: true
        },
        songs: []
      }
    },
    computed: {
      swiper () {
        return this.$refs.mySwiper.swiper
      }
    },
    created () {
      axios.get('http://localhost:3000/top/playlist?limit=10&order=new').then(res => {
        console.log('res', res)
        if (res.status === 200) {
          this.songs = res.data.playlists
          console.log('songs', this.songs)
        }
      })
    }
  }
</script>

<style scoped lang="less">
.banner{
  height: 280px;
  img{
    width: 100%;
    height: 280px;
    object-fit: cover
  }
}
.songs-list{
  width: 20%;
  padding: 10px;
  float: left;
  img{
    width: 100%
  }
  .item{
    position: relative;
    overflow: hidden;
  }
  .title{
    font-size: 12px;
    color: #777;
    height: 40px;
  }
  .count{
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 20px;
    line-height: 20px;
    font-size: 12px;
    text-align: right;
    padding-right: 10px;
    color: #fff;
    background: linear-gradient(to left, rgba(0,0,0,.3), transparent, transparent);
    i{
      font-size: 12px;
      margin-right: 4px;
    }
  }
  &:hover{
    .count{
      display: none
    }
  }
  .des-box{
    // display: none
    position: absolute;
    top: -50px;
    left: 0;
    right: 0;
    padding: 8px 4px;
    background: rgba(0,0,0,.3);
    height: 50px;
    transition: .2s
  }
  .des{
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
    overflow: hidden;
    font-size: 12px;
    color: #fff
  }
  &:hover{
    .des-box{
      display: block;
      top: 0
    }
  }
}
</style>
