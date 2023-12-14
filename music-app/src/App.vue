<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }}
        </h2>
      </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      current: {
        title: 'SONG TITLE'
      },
      songs: [
        {
          title: 'Summer Party',
          artist: 'Summer',
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
      ]
    }
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
