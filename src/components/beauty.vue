<template>
  <div>
    <div style="margin: 10px;overflow: hidden;" v-for="item in list">
      <masker style="border-radius: 2px;">
        <div class="m-img" :style="{backgroundImage: 'url(' + item.img + ')'}"></div>
        <div slot="content" class="m-title">
          {{item.title}}
          <br/>
          <span class="m-time">{{item.time}}</span>
        </div>
      </masker>
    </div>
    <infinite-loading spinner="waveDots" :on-infinite="onInfinite" ref="infiniteLoading">
      <span slot="no-more">
          <divider>暂无更多数据:)</divider>
      </span>
      <span slot="no-results">
          <divider>暂无数据:)</divider>
      </span>
    </infinite-loading>
  </div>
</template>

<script>
  import { Masker, LoadMore, Divider } from 'vux'
  import InfiniteLoading from 'vue-infinite-loading'

  export default {
    components: {
      Masker,
      LoadMore,
      Divider,
      InfiniteLoading
    },
    data () {
      return {
        list: [{
          title: '洗颜新潮流！人气洁面皂排行榜',
          img: 'http://192.168.1.104:9999/static/img/1.6d204c9.jpg',
          time: '2016-03-19'
        }, {
          title: '美容用品 & 日用品（上）',
          img: 'http://192.168.1.104:9999/static/img/1.6d204c9.jpg',
          time: '2016-04-19'
        }, {
          title: '远离车内毒气，日本车载空气净化器精选，日本车载空气净化器精选',
          img: 'http://192.168.1.104:9999/static/img/1.6d204c9.jpg',
          time: '2016-04-21'
        }],
        count: 0
      }
    },
    methods: {
      onInfinite () {
        setTimeout(() => {
          const temp = [{
            title: '洗颜新潮流！人气洁面皂排行榜',
            img: 'http://192.168.1.104:9999/static/img/1.6d204c9.jpg',
            time: '2016-03-19'
          }, {
            title: '美容用品 & 日用品（上）',
            img: 'http://192.168.1.104:9999/static/img/1.6d204c9.jpg',
            time: '2016-04-19'
          }, {
            title: '远离车内毒气，日本车载空气净化器精选',
            img: 'http://192.168.1.104:9999/static/img/1.6d204c9.jpg',
            time: '2016-04-21'
          }]
          this.list = this.list.concat(temp)
          if (this.count === 2) {
            this.$refs.infiniteLoading.$emit('$InfiniteLoading:complete')
          } else {
            this.count++
            console.log(this.count)
            this.$refs.infiniteLoading.$emit('$InfiniteLoading:loaded')
          }
        }, 3000)
      }
    }
  }
</script>

<style lang="less">
  .m-img {
    padding-bottom: 50%;
    display: block;
    position: relative;
    max-width: 100%;
    background-size: cover;
    background-position: center center;
    cursor: pointer;
    border-radius: 2px;
  }

  .m-title {
    color: #fff;
    text-align: center;
    text-shadow: 0 0 2px rgba(0, 0, 0, .5);
    font-weight: 500;
    font-size: 16px;
    position: absolute;
    left: 0;
    right: 0;
    width: 100%;
    text-align: center;
    top: 50%;
    transform: translateY(-50%);
  }

  .m-time {
    font-size: 12px;
    padding-top: 4px;
    border-top: 1px solid #f0f0f0;
    display: inline-block;
    margin-top: 5px;
  }
</style>
