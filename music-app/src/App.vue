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
          <button class="prev" @click="prev">
            <img src="./assets/icons/controls/rewind-button.png" />
          </button>
          <button class="play" v-if="!isPlaying" @click="play">
            <img src="./assets/icons/controls/play.png" />
          </button>
          <button class="pause" v-else @click="pause">
            <img src="./assets/icons/controls/pause.png" />
          </button>
          <button class="next" @click="next">
            <img src="./assets/icons/controls/forward-button.png" />
          </button>
        </div>
      </section>
      <section class="playlist">
        <h3>Summer Vibes</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="song.src == current.src ? 'song playing' : 'song'"
        >
          {{ song.title }} - {{ song.artist }}
        </button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: "Summer Party",
          artist: "Travis Scott",
          src: require("./assets/mp3/sp.mp3")
        },
        {
          title: "Happy Day",
          artist: "Sia",
          src: require("./assets/mp3/hd.mp3")
        },
        {
          title: "Tokyo Cafe",
          artist: "Tvari",
          src: require("./assets/mp3/ttc.mp3")
        }
      ],
      player: new Audio()
    };
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener("ended", () => this.next());
      this.isPlaying = true;
    },

    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    prev() {
      this.index--;

      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];

      this.play(this.current);
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];

      this.play(this.current);
    }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "sanf-serif";
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
  color: #212121;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 400;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background-color: none;
  border: none;
  outline: none;
  cursor: pointer;
  transition: opacity 0.2s;
}

button:hover {
  opacity: 0.8;
}

.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0 15px;
  border-radius: 10px;
  color: #fff;
  background-color: #cc2e5d;
}

.prev,
.next {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0 15px;
  border-radius: 10px;
  color: #fff;
  background-color: rgba(204, 46, 93, 0.8);
  transition: 0.2s;
}

.prev:hover,
.next:hover {
  background-color: #cc2e5d;
  opacity: 1;
}
.playlist {
  padding: 0 30px;
}

.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .song:hover {
  color: #cc2e5d;
}

.playlist .song.playing {
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
}
</style>
