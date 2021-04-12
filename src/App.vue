<template>

    <div id="app">
        <Header />

      <main>
        <section class="player">
          <h1 class="song-title">
          <img class="eventImage" src="./assets/arquivo-de-musica.png" />{{current.title}}
           </h1>
           <p class="artist-song"><img class="userInfo" src="./assets/singer.png" />{{current.artist}}</p>
 
          
          <div class="control">
            <button class="prev" @click="prev">Prev</button>
            <button class="play"  v-if="!isPlaying" @click="play">Play</button>
            <button class="Pause" v-else @click="pause">Pause</button>
            <button class="next" @click="next">Next</button>
          </div>
        </section>

        <section class="playlist">
          <h3>Playlist</h3>
          <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
              {{song.title}} - {{song.artist}}
          </button>
        </section>
     </main>

    <Footer />

    </div>
</template>

<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Footer
  },
  data(){
    return{
      isPlaying: false,
      title:'My songs',
      current:{},
      index: 1,
      songs:[
        {
          title:'I cold be the one',
          artist: 'Avice vs Nicky Romero',
          src: require('./assets/Icoldbetheone.mp3')
        },
        {
          title:'Litle bad',
          artist: 'David guetta',
          src: require('./assets/littlebad.mp3')
        },
        {
          title:'I am wrong',
          artist: 'Nico Vinz',
          src: require('./assets/wrong.mp3')
        },
          {
          title:'Pumped Up of kicks',
          artist: 'Foster the people',
          src: require('./assets/pumped.mp3')
        },
        {
          title:'One day',
          artist: 'Asaf Avidan',
          src: require('./assets/oneday.mp3')
        },
        {
          title:'Sweet Nothing',
          artist: 'Calvin Harris ft Florence Welch',
          src: require('./assets/sweet.mp3')
        },

      ],
      player: new Audio()
    }
  },
  created(){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  // this.player.play();
  },
  methods:{
    play (song){
      if (typeof song.src != "undefined"){
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener('ended', function (){
        this.index++;
        if(this.index < 0){
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);

      }.bind(this))
      this.isPlaying = true;
    },
    pause (){
      this.player.pause();
      this.isPlaying = false;
    },
    next(){
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev(){
     this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  }
}
</script>

<style>
html::-webkit-scrollbar{
    width:9px;
}

html::-webkit-scrollbar-track{
    background: #000;
}

html::-webkit-scrollbar-thumb{
    background: #FF5858;
}

*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background:linear-gradient(to bottom, #3d0254,#180221)
}
main{
  width: 100%;
  margin:0 auto;
  max-width: 760px;
  padding:20px;
}
.song-title{
  color:#fff;
  font-size: 24px;
  text-align: center;
  font-style:italic;
  font-weight: lighter;
  display:flex;
  align-items: center;
  justify-content: center;
}

.song-title span{
  font-weight: 400;
  font-style: italic;
}
.control{
  display:flex;
  justify-content: center;
  padding: 30px 15px;
  align-items: center;
}
button{
  appearance: none;
  background:none;
  border:none;
  outline: none;
  cursor: pointer;
  transition:0.2s ease-in;
}
.play, .Pause{
  font-size:20px;
  font-weight: 70px;
  padding:11px 25px;
  margin:0px 15px;
  border-radius: 8px;
  color:#fff;
  border:2px solid rgba(0,0,0,0.4);
}
.play{
  background-color: rgb(43, 79, 187);
}
.play:hover{
  background-color: rgb(6, 17, 53);
}
.Pause{
    background: #f68a5f;
}
.Pause:hover{
   background-color: rgb(223, 130, 24);
}
.next, .prev{
  border:2px solid rgba(0,0,0,0.4);
  font-size:17px;
  font-weight: 70px;
  padding:10px 20px;
  margin:0px 15px;
  border-radius: 8px;
  color:#fff;
  background: #FF5858;
}
.next:hover, .prev:hover{
   background: #310303;
}
h1 span{
  display:block;
  font-size: 20px;
  text-transform: none;
  padding:4px 0px;
}
.playlist{
  padding: 0px 30px;
}
.playlist h3{
  color:#fff;
  font-size:28px;
  font-weight: 400;
  margin-bottom:30px;
  text-align: center;
}
.playlist .song{
  margin:9px 0;
  display:block;
  width: 100%;
  padding:15px;
  font-size: 14px;
  font-weight: 700;
  cursor: pointer;
  border:2px solid rgba(0,0,0,0.4);
  background:rgba(0,0,0,0.3);
  box-shadow: 1px 1px 1px 1px rgba(0,0,0,0.1);
  color:snow;
  transition:0.7s ease-in-out;
} 
.playlist .song:hover{
  color:#212121;
  background: linear-gradient(to right, #84b6a9, #9c5a5a);
}
.playlist .song.playing{
  color:#fff;
  background: linear-gradient(to right, #CC2E50, #FF5858);
  border:2px solid rgba(199, 44, 44, 0.822);
}
.eventImage{
  margin-right:8px;
}
.artist-song{
  color:#fff;
  text-align: center;
  font-size: 18px;
  margin-top: 5px;
}
.userInfo{
  font-size:15px;
  width:18px;
  margin-right:8px;
}
</style>
