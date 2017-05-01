<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menuWrapper">
      <ul class="menu-list">
        <li class="menu-item" v-for='(item,index) in goods' :class="{current:index === currentIndex}"
            @click="test">
          <span class="text border-1px"><span v-if="item.type>=0" class="icon"
                                              :class="classMap[item.type]"></span>{{item.name}}</span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodsWrapper">
      <ul class="foods-list">
        <li class="foods-list-item food-list-hock" v-for="(items,index) in goods">
          <div class="title">{{items.name}}</div>
          <ul>
            <li v-for="item in items.foods" class="foodItem">
              <div class="foodDetail">
                <span class="foodImg"><img :src="item.icon" class="foodIcon" width="57" height="57"></span>
                <span class="foodmsg">
                  <div class="foodName">{{item.name}}</div>
                  <div class="foodDescript greyFont" :v-if="item.description !== ''">{{item.description}}</div>
                  <div class="sellRating greyFont">
                    <span class="sellCount">月售{{item.sellCount}}份</span><span class="rating">好评率{{item.rating}}%</span>
                  </div>
                  <span class="foodPrice">¥{{item.price}}</span>
                  <span v-if="item.oldPrice !== ''" class="foodOldPrice greyFont">¥{{item.oldPrice}}</span>
                </span>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll';

  export default{
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        goods: [],
        classMap: ['discount', 'decrease', 'guarantee', 'invoice', 'special'],
        foodsHeight: [],
        scroll: 0
      };
    },
    created () {
      this.$http.get('api/goods').then((res) => {
        if (res.body.errno === 0) {
          this.goods = res.body.data;
        }
      });
      this.$nextTick(() => {
        setTimeout(this.initScroll, 100);
        setTimeout(this.calcuHeight, 200);
      });
    },
    methods: {
      initScroll () {
        this.menuScroll = new BScroll(this.$refs.menuWrapper);
        this.foodScroll = new BScroll(this.$refs.foodsWrapper, {
          probeType: 3
        });
        this.foodScroll.on('scroll', (pos) => {
          this.scroll = Math.abs(Math.round(pos.y));
        });
      },
      calcuHeight () {
        let foodList = this.$refs.foodsWrapper.getElementsByClassName('food-list-hock');
        let height = 0;
        this.foodsHeight.push(height);
        for (let i = 0; i < foodList.length; i++) {
          height += foodList[i].clientHeight;
          this.foodsHeight.push(height);
        }
      },
      selectMenu (index, event) {
        let foodList = this.$refs.foodsWrapper.getElementsByClassName('food-list-hock');
        this.foodScroll.scrollToElement(foodList[index], 1000);
      },
      test () {
        console.log(11);
      }
    },
    computed: {
      currentIndex () {
        for (let i = 0; i < this.foodsHeight.length; i++) {
          let h1 = this.foodsHeight[i];
          let h2 = this.foodsHeight[i + 1];
          if (this.scroll >= h1 && this.scroll < h2) {
            return i;
          }
        }
        return 0;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/mixin.styl'
  .goods
    display flex
    font-size 0px
    position absolute
    top 176px
    bottom 46px
    overflow hidden
    width 100%
    .menu-wrapper
      flex 0 0 80px
      width 80px
      height 100%
      background-color #f3f5f7
      .menu-list
        .current
          position relative
          top -1px
          background-color rgb(255, 255, 255)
          font-weight 700
          z-index 20
          & > .text:after
            display none
        .menu-item
          width 56px
          height 54px
          display table
          padding 0 12px
          .text
            font-size 12px
            line-height 14px
            display table-cell
            vertical-align middle
            color rgb(7, 17, 27)
            .icon
              display inline-block
              background-size 12px 12px
              background-repeat no-repeat
              width 12px
              height 12px
              margin-right 2px
              vertical-align top
            .discount
              bg-img('discount_3');
            .decrease
              bg-img('decrease_3');
            .guarantee
              bg-img('guarantee_3');
            .invoice
              bg-img('invoice_3');
            .special
              bg-img('special_3');
        .menu-item:not(:last-child)
          & > .text
            border-1px(rgba(7, 17, 27, 0.1))
    .foods-wrapper
      flex 1
      overflow hidden
      .title
        padding-left 14px
        height 26px
        font-size 12px
        color: rgb(147, 153, 159)
        line-height 26px
        background-color #f3f5f7
        border-left 2px solid #d9dde1
      .foodItem
        padding 18px
        padding-bottom 0px
        font-size 0px
        .foodDetail
          display flex
          padding-bottom 18px
          .foodmsg
            display inline-block
            .foodDescript
              line-height 14px
          .foodImg
            display inline-block
            width 70px
            height 70px
            margin-right 10px
            overflow hidden
            flex 0 0 57px
          .foodName
            display inline-block
            font-size 16px
            color rgb(7, 17, 27)
            line-height 14px
            margin-top 2px
          .sellRating
            display table
            .sellCount
              display table-cell
              vertical-align middle
            .rating
              display table-cell
              vertical-align middle
          .greyFont
            margin-top 8px
            font-size 10px
            line-height 10px
            color rgb(147, 153, 159)
          .foodPrice
            display inline-block
            color rgb(240, 20, 20)
            font-weight 700
            line-height 24px
            font-size 14px
          .foodOldPrice
            font-weight 700
            margin-left 8px
            font-size 10px
      .foodItem:not(:last-child)
        & > .foodDetail
          border-1px(rgba(7, 17, 27, 0.1))
</style>
