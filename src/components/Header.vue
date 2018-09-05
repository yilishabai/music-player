<template>
  <div>
    <h1>Music Player</h1>
    <img src="../assets/image.png">
    <input type="file" accept="mp3/mp4" ref="music">
    <button @click="handleClick">确认</button>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      src: ""
    }
  },
  methods: {
  	handleClick: function() {
      var reader = new FileReader();
      let file = this.$refs.music.files[0]
      console.log(file)
      reader.onload = e => {
        this.$emit("changeMusicSrc", e.target.result);
      };
      if (file) {
        reader.readAsDataURL(file);
      }
      //this.$emit("changeMusicSrc", this.src)
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
