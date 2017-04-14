<template>
  <div id="header">
    <div id="bgBlur">
      <img :src="seller.avatar">
    </div>
    <div id="info">
      <div id="avatar">
        <img :src="seller.avatar">
      </div>
      <div id="store">
        <div id="brand"></div>
        <span id="name">{{seller.name}}</span>
        <div id="sendWay">{{seller.description}}/{{seller.deliveryTime}}分钟到达</div>
        <div v-if='seller.supports' id="disc">
          <span id="icon" :class="disc[seller.supports[0].type]"></span>
          <span id="description">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" id="flowLayer" @click="showDetail = true">
        <span id="count">{{seller.supports.length}}个</span><i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div id="notice" @click="showDetail = true">
      <span id="noticeIcon"></span><span id="noticeContext">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <transition name="fade">
      <div id="detail" v-show="showDetail">
        <div class="wrap clear-flow">
          <div class="main clear-flow">
            <div class="name">{{seller.name}}</div>
            <star :size=48 :score=seller.score class="star"></star>
            <div class="content">
              <span class="line"></span>
              <span class="msg">优惠信息</span>
              <span class="line"></span>
            </div>
            <ul class="disMsg" v-if="seller.supports">
              <li class="disMsgItem" v-for="discItem in seller.supports">
                <span class="icon" :class="disc[discItem.type]"></span>
                <span class="disMsgItemContent">{{discItem.description}}</span>
              </li>
            </ul>
            <div class="content">
              <span class="line"></span>
              <span class="msg">商家广告</span>
              <span class="line"></span>
            </div>
            <p class="storeContent">{{seller.bulletin}}</p>
          </div>
        </div>
        <div class="detailClose" @click='showDetail = false'><i class="icon-close"></i></div>
      </div>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from '../star/star.vue';

  export default{
    data () {
      return {
        showDetail: false,
        disc: ['discount', 'decrease', 'guarantee', 'invoice', 'special']
      };
    },
    props: {
      seller: {
        type: Object
      }
    },
    components: {
      star
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/mixin.styl'
  #header
    font-size: 0px
    color: #fff
    position: relative
    overflow hidden
    padding: 24px 0px 0px
    background-color: rgba(7, 17, 27, 0.5)
    #bgBlur
      width: 100%
      height: 100%
      position: absolute
      top: 0
      left: 0
      z-index: -1
      filter: blur(10px)
      overflow hidden
      img
        width 100%
        height 100%
    #info
      display: inline-block
      margin-top: 2px
      margin-left: 16px
      width: 100%
      #flowLayer
        height: 24px
        border-radius: 14px
        right: 12px
        bottom: 45px
        position: absolute
        line-height: 24px
        padding: 0 8px
        background-color: rgba(0, 0, 0, 0.2)
        #count
          font-size: 10px
          line-height: 24px
          vertical-align middle
        .icon-keyboard_arrow_right
          margin-left: 2px
          font-size: 10px
          line-height: 24px
          vertical-align middle
      #avatar
        display: inline-block
        width: 64px
        height: 64px
        vertical-align: top
        margin-bottom: 18px
        & > img
          border-radius: 4px
          width: 64px
          height: 64px
      #store
        display inline-block
        margin-left: 16px
        padding-top: 2px
        #brand
          width: 30px
          height: 18px
          display: inline-block
          bg-img('brand');
          vertical-align: top
          background-size: 30px 18px
          background-repeat: no-repeat
          margin-right: 6px
          margin-bottom: 8px
        #name
          vertical-align: top
          display: inline-block
          font-size: 16px
          font-weight: bold
          line-height: 18px
        #sendWay
          font-size: 12px
          line-height: 12px
          margin-bottom: 10px
        #disc
          & > #icon
            display: inline-block
            width: 12px
            height: 12px
            background-size: 12px 12px
            background-repeat: no-repeat
            vertical-align: top
            margin-right: 4px
          & > .decrease
            bg-img('decrease_1')
          & > .discount
            bg-img('discount_1')
          & > .guarantee
            bg-img('guarantee_1')
          & > .invoice
            bg-img('invoice_1')
          & > .special
            bg-img('special_1')
          #description
            font-size: 10px
            line-height: 12px
            display: inline-block
    #notice
      height: 28px
      font-size 10px
      line-height: 28px
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      padding: 0 22px 0 12px
      position: relative
      background-color: rgba(7, 17, 27, 0.2)
      #noticeIcon
        display: inline-block
        width: 22px
        height: 12px
        bg-img('bulletin')
        background-size: 22px 12px
        margin-top: 8px
        vertical-align: top
      #noticeContext
        font-size: 10px
        vertical-align: top
        margin: 0 4px
      .icon-keyboard_arrow_right
        font-size: 10px
        position: absolute
        right: 12px
        top: 9px

  #detail
    position: fixed
    top: 0px
    left: 0px
    width 100%
    height 100%
    background-color: rgba(7, 17, 27, 0.8)
    z-index :100
    .wrap
      min-height 100%
      height: auto
      overflow:auto
      zoom :1
      .main
        padding-bottom: 64px
        .name
          text-align: center
          margin: 64px 0px 16px 0px
          font-size: 16px
          font-weight: 700
          line-height 16px
        .star
          text-align: center
        .content
          display: flex
          width: 80%
          margin: 28px auto 24px auto
          .line
            display: inline-block
            flex: 1
            height: 1px
            background-color: rgba(255, 255, 255, 0.2)
            position: relative
            top: 6px
          .msg
            font-weight: 700
            margin: 0px 24px
            font-size: 16px
        .disMsg
          list-style: none
          font-size: 12px
          font-weight: 100
          line-height: 16px
          width: 80%
          margin: 0 auto
          display: block
          .disMsgItemContent
          .disMsgItem
            margin-bottom: 12px
            vertical-align: middle
          .icon
            display: inline-block
            width: 16px
            height: 16px
            background-size 16px 16px
            margin-right: 6px
            vertical-align: middle
          &:last-child
            margin-bottom: 0px
          .discount
            bg-img('discount_2');
          .decrease
            bg-img('decrease_2');
          .guarantee
            bg-img('guarantee_2');
          .invoice
            bg-img('invoice_2');
          .special
            bg-img('special_2');
        .storeContent
          margin: 0 auto
          width: 80%
          font-size: 12px
          line-height: 24px
    .detailClose
      position relative
      clear: both
      width: 32px
      height: 32px
      font-size: 32px
      margin:-64px auto 0px auto
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s
  }
  .fade-enter, .fade-leave-active {
    opacity: 0
  }
</style>
