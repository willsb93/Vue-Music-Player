<template>
  <div id="app">
    <header>
      <h1>My music player</h1>
    </header>
    <main>
        <section class="player">
            <h2 class = "song-title">{{currentSong.title}} - <span>{{currentSong.artist}}</span></h2>
            <div class="controls">
              <button class = "prev" @click="prev">Prev</button>
              <button class = "play" v-if = !isPlaying @click="play">Play</button>
              <button class = "pause" v-else @click="pause">Pause</button>
              <button class = "next" @click="next">Next</button>
            </div>
          </section>
          <section class = "playlist">
            <h4>Sample Playlist</h4>
            <button v-for = "song in songs" :key= "song.src" @click = play(song) :class = "(song.src == currentSong.src) ? 'song playing' : 'song'">
              {{song.title}} - {{song.artist}}</button>
          </section>
          <div><a href = "https://www.bensound.com/" target="_blank"> Royalty Free Music from Bensound </a></div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      currentSong: {},
      index: 0,
      isPlaying: false,
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
  methods: {
    play(song){
        if (typeof song.src != "undefined") {
          this.current = song;
          this.player.src = this.current.src;
        }
        this.player.play();
        this.player.addEventListener ("ended", function (){
          this.index++;
          if (this.index > this.songs.length - 1) {
            this.index = 0;
          }

          this.currentSong = this.songs[this.index];
          this.play(this.current);
        }.bind(this));
        this.isPlaying = true;
    },
   pause () {
        this.player.pause();
        this.isPlaying = false;
   },
   next (){
        this.index++;
        if (this.index > this.songs.length - 1) {
          this.index = 0;
        }
        this.currentSong = this.songs[this.index];
        this.play(this.currentSong);
   },
   prev (){
        this.index--;
        if (this.index < 0) {
          this.index = this.songs.length - 1;
        }
        this.currentSong = this.songs[this.index];
        this.play(this.currentSong);
   }
  },
  created () {
    this.currentSong = this.songs[this.index];
    this.player.src = this.currentSong.src;
    
  }
}
</script>

<style>

* {
  margin: 0;
  padding : 0;
  box-sizing: border-box;
}

body {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
}








</style>
