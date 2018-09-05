<template>
  <div >
    <input
      type="range"
      ref="progress"
      min="0"
      max="100"
      v-model:value="prges"
      :style="'background-size:' + prges + '% 100%'"
    >
  </div>
</template>

<script>
export default{
  props: {
    progress: Number
  },
  name: 'ProgressBar',
  computed: {
    prges: {
      get() {
        return this.progress;
      },
      set(val) {
        this.$emit('progressChange', val)
      }      
    }
  }
}
</script>

<style lang="stylus" scoped>
.line
  height: 5px
  width: 210px
  padding: 0
  background: #fff
  border: 1px solid #9e9e9e
  border-radius: 3px
  position: relative
  .slider
    height: 10px
    width: 10px
    background: #338036
    border-radius: 50%
    position: absolute
    top: -2.5px
    display: inline
  .bar
    height: 5px
    background: #28e830
input[type=range]
  -webkit-appearance: none
  width: 200px
  border-radius: 5px
  background: -webkit-linear-gradient(#28e830, #28e830) no-repeat, #fff;/*设置左边颜色为#612，右边颜色为#ddd*/
  background-size: 55% 100%;/*设置长宽比例*/
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
  height: 10px
  width: 10px
  margin-top: -1px
  background: #338036
  border-radius: 50%
  border: 1px solid #9e9e9e
</style>