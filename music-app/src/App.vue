<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} - 
          <span>
            {{ current.artist }}
          </span>
        </h2>
        <div class="controls">
          <button class="prev">
            Prev
          </button>
          <button class="play" v-if="!isPlaying" @click="play">
            Play
          </button>
          <button class="pause" v-else @click="pause">
            Pause
          </button>
          <button class="next">
            Next
          </button>
        </div>
      </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Summer Party',
          artist: 'Travis Scott',
          src: require('./assets/mp3/sp.mp3')
        },
        {
          title: 'Happy Day',
          artist: 'Sia',
          src: require('./assets/mp3/hd.mp3')
        },
        {
          title: 'Tokyo Cafe',
          artist: 'Tvari',
          src: require('./assets/mp3/ttc.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play(song){
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },

    pause(){
      this.player.pause();
      this.isPlaying = false;
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: "sanf-serif";
}

header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}
</style>
