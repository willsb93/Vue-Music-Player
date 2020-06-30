<template>
  <div id="app">
    <header>
      <h1>My music player</h1>
    </header>
    <main>
        <section class="player">
            <h2 class = "song-title">{{currentSong.title}} - <span>{{currentSong.artist}}</span></h2>
        </section>
    </main>
  
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      currentSong: {
        title: "Song Title"
      },
      index: 0,
      songs: [
        {
          title: "Dance",
          artist: "bensound",
          src: require ("./assets/bensound-dance.mp3")
        },
        {
          title: "Dreams",
          artist: "bensound",
          src: require ("./assets/bensound-dreams.mp3")
        },
        {
          title: "Dubstep",
          artist: "bensound",
          src: require ("./assets/bensound-dubstep.mp3")
        },
        {
          title: "Endlessmotion",
          artist: "bensound",
          src: require ("./assets/bensound-endlessmotion.mp3")
        }
      ],
      player: new Audio()
    }
  },
  created () {
    this.currentSong = this.songs[this.index];
    this.player.src = this.current.src;
  }
}
</script>

<style>

</style>
