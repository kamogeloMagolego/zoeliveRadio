<template>
  <div id="app">
    <!-- <navigation-bar></navigation-bar>  -->
    <div class="header">
      <!-- Your other header content -->
      <h1>ZOElive Radio</h1>

      <div class="volume-control">
        <button @click="muteUnmute" :class="{ 'muted': isMuted }">
          <i v-if="isMuted" class="fas fa-volume-mute" :style="{ color: volumeLevel > 75 ? '#d9534f' : '' }"></i>
          <i v-else-if="volumeLevel === 0" class="fas fa-volume-off"
            :style="{ color: volumeLevel > 75 ? '#d9534f' : '' }"></i>
          <i v-else-if="volumeLevel < 50" class="fas fa-volume-down"
            :style="{ color: volumeLevel > 75 ? '#d9534f' : '' }"></i>
          <i v-else class="fas fa-volume-up" :style="{ color: volumeLevel > 75 ? '#d9534f' : '' }"></i>
        </button>
        <input type="range" min="0" max="100" v-model="volumeLevel" @input="adjustVolume" />
      </div>
    </div>
    <div class="side-bar">
      <sidebar-layout></sidebar-layout>

      <main>
        <section class="player">
          <h2 class="song-title">ZOElive Radio - <span>The Abundant life Experience</span></h2>
          <div class="controls">
            <button class="play" @click="togglePlayStop">
              <i v-if="isPlaying" class="fas fa-stop"></i>
              <i v-else class="fas fa-play"></i>
            </button>
            <audio ref="audioElement" :src="audioSource"></audio>
          </div>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
// import NavigationBar from "./Layouts/NavigationBar.vue";
import SidebarLayout from "./Layouts/SidebarLayout.vue";
export default {
  components: {
    // NavigationBar,
    SidebarLayout,
  },
  name: 'App',
  data() {
    return {
      volumeLevel: 50,
      isMuted: false,
      isPlaying: false,
      audioSource: "https://live.urbanza.co.za/listen/zoeliveradio/zoeliveradio",
    }
  },
  methods: {
    togglePlayStop(){
      const audioElement = this.$refs.audioElement;

      if (this.isPlaying) {
        // Stop the audio
        // audioElement.pause();
        // audioElement.currentTime = 0;
        audioElement.volume = 0;
      } else {
        audioElement.volume = this.volumeLevel * 0.01;
        // Start playing the audio
        audioElement.play();
      }

      this.isPlaying = !this.isPlaying;
    },
    muteUnmute() {
      this.isMuted = !this.isMuted;
      const audioElement = this.$refs.audioElement;
      if(this.isMuted){
        audioElement.volume = 0;
      } else {
        audioElement.volume = this.volumeLevel * 0.01;
      }
    },
    adjustVolume() {
      const audioElement = this.$refs.audioElement;
      audioElement.volume = this.volumeLevel * 0.01;
      // console.log(this.volumeLevel * 0.1);
    },
  },
  created() {
    // this.current = this.songs[this.index];
    // this.player.src = this.current.src;
    // this.player.play();
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

}

.side-bar {
  display: flex;
  height: 100vh;
}

body {
  font-family: sans-serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.song-title {
  color: #53565a;
  font-size: 25px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 200;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

.play {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #cc2e5d;
}

button:hover {
  opacity: 0.8;
}

.header {
  /* display: flex;
  justify-content: space-between; Align items to the far left and far right */
  /* align-items: center; */
  /* Your other header styles */
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}

.header h1 {
  align-items: center;
}

.volume-control {
  display: flex;
  align-items: center;
}

.volume-control button {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.2rem;
  margin-right: 8px;
  color: #fff;
}

.volume-control button.muted {
  color: #d9534f;
}

.volume-control input {
  background-color: #cc2e5d;
  width: 100px;
}
</style>
