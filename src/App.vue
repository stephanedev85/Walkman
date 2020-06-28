<template>
  <div id="app">
    <header>
      <h1>Mon Walkman</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="controls">
          <button class="retour">Retour</button>
          <button class="play" v-if="!isPlaying" @click="play">Lecture</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="avancer">Avancer</button>
        </div>
      </section>
      <section class="playlist">
        <h3>Liste de lecture</h3>
        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'la musique commence' : 'song'">

          {{ song.title }}
        </button>
      </section>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data (){
    return{
      current: {},
      index: 0,
      isPlaying: false,
      songs: [ 
      {
        title: 'jah live',
        artist: 'Bob Marley',
        src: require('./assets/bob-marley-jah-live.mp3')
      },
      {
         title: 'the man who sold the world',
        artist: 'Nirvana',
        src: require('./assets/nirvana.mp3')
      },
      {
         title: 'english man in new york',
        artist: 'Sting',
        src: require('./assets/sting.mp3')
      }
      ],
      player: new Audio()
    }
  },
  methods:{
     play (song) {
       if (typeof song.src != "undefined"){
         this.current = song;

         this.player.src = this.current.src
       }
       this.player.play();
       this.isPlaying = true;
     },
     pause (){
       this.player.pause();
       this.isPlaying = false;
     }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
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
  font-family: sans-serif;
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
