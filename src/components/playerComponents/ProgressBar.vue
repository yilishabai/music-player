<template>
  <div >
    <div
      class="line"
      @click="sliderMouseup"
    >
      <div
        class="slider"
        ref="slider"
        :style="'left:'+ progress * 2 + 'px'"
      ></div>
      <div
        class="bar"
        :style="'width:'+ progress * 2 + 'px'"
      ></div>
    </div>
  </div>
</template>

<script>
export default{
  props: {
    progress: Number
  },
  name: 'ProgressBar',
  data() {
    return {
      clickX: 0,
      moveX: 0,
      click: false,
    }
  },

  methods: {
    sliderMouseup: function(e){
      this.click = false
      this.clickX=Math.floor(e.offsetX/2.1)
      this.$emit('progressChange', this.clickX)
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
</style>