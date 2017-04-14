<template>
  <div class="startDiv" :class='starType'>
    <span v-for="item in items" class="starItem" :class='item' ></span>
  </div>
</template>

<script type="text/ecmascript-6">
  const LENGTH = 5;
  const ON = 'on';
  const HALF = 'half';
  const OFF = 'off';
  export default{
    props: {
      size: {
        type: Number
      },
      score: {
        type: Number
      }
    },
    computed: {
      starType () {
        return 'star-' + this.size;
      },
      items () {
        let result = [];
        let star, index;
        star = Math.floor(this.score * 2) / 2;
        index = this.score % 1 !== 0;
        for (let i = 0; i < star; i++) {
          result.push(ON);
        }
        if (index) {
          result.push(HALF);
        }
        while (result.length < LENGTH) {
          result.push(OFF);
        }
        return result;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/mixin.styl'

  .startDiv
    font-size: 0
    .starItem
      display: inline-block
      background-repeat: no-repeat
    &.star-24
      .starItem
        width: 10px
        height: 10px
        margin-right: 3px
        background-size: 10px 10px
        &:last-child
          margin-right: 0px
        &.on
          bg-img('star24_on')
        &.off
          bg-img('star24_off')
        &.half
          bg-img('star24_half')
    &.star-36
      .starItem
        width: 15px
        height: 15px
        margin-right: 7px
        background-size: 15px 15px
        &:last-child
          margin-right: 3px
        &.on
          bg-img('star36_on')
        &.off
          bg-img('star36_off')
        &.half
          bg-img('star36_half')
    &.star-48
      .starItem
        width: 20px
        height: 20px
        display: inline-block
        margin-right: 22px
        background-size: 20px 20px
        &:last-child
          margin-right: 0px
      .on
        bg-img('star48_on')
      .off
        bg-img('star48_off')
      .half
        bg-img('star48_half')


</style>
