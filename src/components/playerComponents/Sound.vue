<template>
  <div>
    <span 
      class="iconfont sound"
      @click="handleClick"
    >
      {{sound? '&#xe62c;' : '&#xe61e;'}}
    </span>
    <input
      type="range"
      min="0"
      max="100"
     >
  </div>
</template>

<script>
export default{
  props: {
   sound: Boolean
  },
  name: 'SoundSet',
  methods: {
    handleClick: function () {
      this.$emit('changeSound')
    }
  }
}
</script>

<style lang="stylus" scoped>
input[type=range]
  -webkit-appearance: none
  width: 100px
  border-radius: 10px
  background: -webkit-linear-gradient(#61bd12, #61bd12) no-repeat, #fff;/*设置左边颜色为#612，右边颜色为#ddd*/
  background-size: 55% 100%;/*设置左右宽度比例*/
input[type=range]::-webkit-slider-thumb
  -webkit-appearance: none
input[type=range]::-webkit-slider-runnable-track 
  height: 10px
  border-radius: 5px
  border: 1px solid #000
input[type=range]:focus
  outline: none
input[type=range]::-webkit-slider-thumb 
  -webkit-appearance: none
  height: 15px
  width: 15px
  margin-top: -2.5px
  background: #ffffff 
  border-radius: 50%
  border: 1px solid #000
input[type=range]:focus:-webkit-slider-thumb
  background: #338036
</style>