<template>
  <div id="app">
    <Header @changeMusicSrc="changeMusicSrc" />
    <Player :musicSrc="musicSrc"/>
  </div>
</template>

<script>
import Header from './components/Header'
import Player from './components/Player'
export default {
  name: 'App',
  data() {
  	return {
  	  musicSrc:"./assets/music.mp3"
  	}
  },
  methods: {
    changeMusicSrc: function(musicSrc){
      console.log(musicSrc)
      this.musicSrc=musicSrc;
    }
  },
  components: {
    Header,
    Player
  }
}
</script>

<style>
@import './assets/iconfont.css';
</style>
