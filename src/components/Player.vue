<template>
  <div>
    <audio
      ref="player"
      src="../assets/music.mp3"
      style="display: none"
      controls>
    </audio>
    <button @click="startstop()">{{this.start?'start':'stop'}}</button>
    <div class="progress">
      {{ timeNowString }}
      <div class="progressBar">
        <progress-bar
          :progress="progress"
          @progressChange="progressChange"
        ></progress-bar>
      </div>
      {{ timeDurationString }}
    </div>
    <button @click="ifSound()">{{sound?'sound':'nosound'}}</button>
  </div>
</template>

<script>
import ProgressBar from './playerComponents/ProgressBar'
export default {
  name: 'Player',
  components: {
    ProgressBar
  },
  data () {
    return {
      timeNow: 0,
      timeDuration: 0,
      sound: true,
      start: true
    }
  },
  computed: {
    progress: {
      get(){
      	return Math.round((this.timeDuration?this.timeNow/this.timeDuration:0)*100);
      },
      set(newValue){
        const self = this;
        self.timeNow = Math.round(newValue*self.timeDuration/100);
        self.$refs.player.currentTime = self.timeNow;
      }      
    },
    timeNowString: function() {
      const self = this;
      return Math.floor(self.timeNow/60)+':'+(self.timeNow%60<10?'0'+self.timeNow%60:self.timeNow%60)
    },
    timeDurationString: function() {
      const self = this;
      return Math.floor(self.timeDuration/60)+':'+(self.timeDuration%60<10?'0'+self.timeDuration%60:self.timeDuration%60)
    }
  },
  methods: {
  	startstop: function(){
      const self = this;
      let player = self.$refs.player;
      if(player.paused)
      	player.play();
      else
      	player.pause();
      this.start = player.paused
  	},
  	ifSound: function(){
  	  const self = this;
      let player = self.$refs.player;
      player.muted=this.sound;
      this.sound=!this.sound;
  	},
    progressChange: function(value){
      console.log(value)
      this.progress=value
    },
    addEventListeners: function () {
      const self = this;
      self.$refs.player.addEventListener('timeupdate', self._currentTime),
      self.$refs.player.addEventListener('canplay', self._durationTime)
    },
    removeEventListeners: function () {
      const self = this;
      self.$refs.player.removeEventListener('timeupdate', self._currentTime)
      self.$refs.player.removeEventListener('canplay', self._durationTime)
    },
    _currentTime: function () {
      const self = this;
      self.timeNow = parseInt(self.$refs.player.currentTime)
    },
    _durationTime: function () {
      const self = this;
      self.timeDuration = parseInt(self.$refs.player.duration)
    }
  },
  mounted() {
    this.addEventListeners()
  },
  beforeDestroyed() {
    this.removeEventListeners();
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.progress
  margin: 10px
  .progressBar
    display: inline-block
    padding-bottom: 2px
</style>
