<template>
  <b-container fluid>
    <!--Nom de l'application et logo-->
    <header class="header">
      <h1>Music App</h1>
    </header>
    <!--Section où tout se joue-->
    <div class="main">
      <section>
        <!--Titre du son en cours de lecture, étant une variable, il change automatiquement-->
        <h2 class="song-title">{{ current.title }}</h2>
        <div class="container">
          <!--Intégration de la vidéo-->
          <video width="400px" height="200px" src="@/assets/Anonymous-Girl-Face-Live-Wallpaper.mp4" autoplay></video>
        </div>
      </section>
      <!--Les controls du lecteur de musique-->
      <div class="controls">
        <button class="btn btn-danger prev" style="margin: 1px;" @click="prev">Prev</button>
        <button class="btn btn-danger pause" style="margin: 1px;" v-if="isPlaying" @click="pause">Pause</button>
        <button class="btn btn-danger play" style="margin: 1px;" v-else @click="play">Play</button>
        <button class="btn btn-danger next" style="margin: 1px;" @click="next">Next</button>
      </div>
      <b-list-group class="playlist">
        <h3>The Playlist</h3>
        <!--La liste des musiques-->
        <button class="btn btn-danger" style="margin: 2px;" v-for="(song, index) in songs" :key="index" @click="play(song)" :class="(song.src == current.src)? 'song-playing' : 'song'">
          {{ song.title }}
        </button>
      </b-list-group>
    </div>
    <h6>Music: https://www.bensound.com/</h6>
  </b-container>
</template>

<script>
export default {
  name: 'Music',
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false, //Aide à vérifier si le morceau doit être mis en pause ou lancer
      //liste des morceaux
      songs: [
        {
        title: 'bensound-groovy',
        src: require('@/assets/bensound-groovyhiphop.mp3')
        },
        {
        title: 'bensoud-hey',
        src: require('@/assets/bensound-hey.mp3')
        },
        {
        title: 'bensoud-funckyelement',
        src: require('@/assets/bensound-funkyelement.mp3')
        },
        {
        title: 'bensoud-cute',
        src: require('@/assets/bensound-cute.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    //fonction de lancement de la musique, attribué au bouton Play
    play(song) {
      if (typeof song.src !== "undefined"){
        this.current = song;

        this.player.src = this.current.src;
      }

      this.player.play();
      this.isPlaying = true;
    },
    //fonction de pause de la musique, attribué au bouton Pause
    pause(){
      this.player.pause();
      this.isPlaying = false;
    },
    //fonction pour jouer le morceau précédent, attribué au bouton Prev
    prev(){
      this.index--
      if (this.index < 0) {
        this.index = this.songs.length - 1
      }

      this.current = this.songs[this.index]
      this.play(this.current)
    },
    //fonction pour jouer le morceau suivant, attribué au bouton Next
    next(){
      this.index++
      if (this.index > this.songs.length - 1) {
        this.index = 0
      }

      this.current = this.songs[this.index]
      this.play(this.current)
    }
  },
  created() {
    this.current = this.songs[this.index]
    this.player.src = this.current.src
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  width: 100%;
  color: white;
}
</style>
