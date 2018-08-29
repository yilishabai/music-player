<template>
  <div>
    <audio
      ref="player"
      src="../assets/music.mp3"
      style="display: none"
      controls>
    </audio>
    <button @click="startstop()">start/stop</button>
    <p>{{ timeNowString }}-{{ timeDurationString }}</p>
    <div class="progressBar">
      <input type="range" min="0" max="100" v-model:value=progress />
    </div>
    <button @click="ifSound()">{{sound?'sound':'nosound'}}</button>
  </div>
</template>

<script>
export default {
  name: 'Player',
  data () {
    return {
      timeNow: 0,
      timeDuration: 0,
      sound: true
    }
  },
  computed: {
    progress: {
      get(){
      	return Math.round((this.timeDuration?this.timeNow/this.timeDuration:0)*100);
      },
      set(newValue){
        const self = this;
        self.timeNow = newValue*self.timeDuration/100;
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
  	},
  	ifSound: function(){
  	  const self = this;
      let player = self.$refs.player;
      player.muted=this.sound;
      this.sound=!this.sound;
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
<style scoped>

</style>
