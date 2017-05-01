<template>
  <div class="shop-cart_wrapper">
    <div class="content-left">
      <div class="logo-wrapper">
        <div class="logo">
          <i class="icon-shopping_cart"></i>
        </div>
      </div>
      <span class="price">¥20</span>
      <span class="deliver-price">另需配送费¥{{seller.deliveryPrice}}</span>
    </div>
    <div class="content-right">
      <span class="shop-cart_btn">{{}}</span>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
      seller: {
        type: Object
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .shop-cart_wrapper
    width 100%
    height 48px
    background #141d27
    display flex
    justify-content space-between
    position absolute
    left 0px
    bottom 0px
    font-size 0px
    .content-left
      display flex
      .logo-wrapper
        margin-left 15px
        border-radius 50%
        background-color #141d27
        width 56px
        height 56px
        margin-top -10px
        padding 6px
        box-sizing border-box
        .logo
          width 44px
          height 44px
          text-align center
          border-radius 50%
          background-color #2B343C
          .icon-shopping_cart
            font-size 24px
            color rgba(255, 255, 255, 0.4)
            line-height 44px
      .price
        color rgba(255, 255, 255, 0.4)
        font-size 16px
        line-height 23px
        font-weight 700
        margin 11px 0px 12px 12px
        border-right 1px solid rgba(255, 255, 255, 0.1)
        padding-right 12px
      .deliver-price
        font-size 12px
        margin-left 12px
        color rgba(255,255,255,0.4)
        line-height 48px
    .content-right
      flex 0 0 105px
      width 105px
      background-color rgb(43, 51, 59)
      padding 0 8px
      box-sizing border-box
      margin-left 12px
      text-align center
      .shop-cart_btn
        font-size 12px
        color rgba(255, 255, 255, 0.4)
        font-weight 700
        line-height 46px
</style>
