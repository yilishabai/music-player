<template>
  <div class="volumeBlock">
    <span 
      class="iconfont sound"
      @click="handleClick"
    >
      {{sound? '&#xe62c;' : '&#xe61e;'}}
    </span>
    <input
      type="range"
      ref="volume"
      min="0"
      max="100"
      v-model:value="volume"
      :style="'background-size:' + volume + '% 100%'"
    >
    <div class="volumeNumber">{{volume}}</div>
  </div>
</template>

<script>
export default{
  props: {
   sound: Boolean
  },
  name: 'SoundSet',
  data() {
    return {
     volume: 80
    }
  },
  methods: {
    handleClick: function () {
      if(this.volume != 0) {
        this.volume = 0;
        this.$emit('changeSound');
      }
    }
  },
  watch: {
    volume: function() {
      this.$emit('changeVolume', this.volume)
    }
  }
}
</script>

<style lang="stylus" scoped>
input[type=range]
  -webkit-appearance: none
  width: 80px
  border-radius: 5px
  background: -webkit-linear-gradient(#61bd12, #61bd12) no-repeat, #fff;/*设置左边颜色为#612，右边颜色为#ddd*/
  background-size: 55% 100%;/*设置长宽比例*/
input[type=range]::-webkit-slider-thumb
  -webkit-appearance: none
input[type=range]::-webkit-slider-runnable-track 
  height: 17px
  border-radius: 5px
  border: 1px solid #000
input[type=range]:focus
  outline: none
input[type=range]::-webkit-slider-thumb 
  -webkit-appearance: none
  height: 0px
  width: 0px
.volumeBlock
  height: 34px
  width: 150px
  position: absolute
  .volumeNumber
    position: absolute
    top: 6px
    right: 10px
</style>