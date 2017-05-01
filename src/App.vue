<template>
  <div id="app">
    <v-header :seller='seller'></v-header>
    <div id="tab" class="border-1px">
      <router-link class="tabitem" to="/goods">商品</router-link>
      <router-link class="tabitem" to="/ratings">评价</router-link>
      <router-link class="tabitem" to="/seller">商家</router-link>
    </div>
    <router-view></router-view>
    <shopcart :seller="seller"></shopcart>
  </div>
</template>

<script>
  import header from './components/header/header';
  import shopcart from './components/shopCart/shopCart';

  export default {
    components: {
      'v-header': header,
      shopcart
    },
    data () {
      return {
        seller: {}
      };
    },
    created () {
      this.$http.get('api/seller').then((res) => {
        this.seller = res.body.data;
      });
    }
  };

</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin"
  #tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(rgba(7, 17, 27, 0.2))
    .tabitem
      flex: 1
      display: block
      text-align: center
      height: 40px
      font-size: 14px
      line-height: 40px
      color: rgb(77, 85, 93)
    .active
      color: rgb(240, 20, 20)

</style>
