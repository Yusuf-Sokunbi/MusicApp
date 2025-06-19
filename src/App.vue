<template>
  <div id="app">
   <header>
    <h1>Music App</h1>
   </header>
   <main>
    <div>{{ current.title }}</div>
    <div>
      <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
      <div class="control">
        <button class="prev" @click="prev">Prev</button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else @click="pause">Pause</button>
        <button class="next" @click="next">Next</button>
      </div>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button v-for="song in songs" :key="song.music" @click="play(song)" :class="(song.music == current.music) ? 'song playing' : 'song'">
       {{ song.title }}
        </button>
      </section>
      <!-- <ul>
        <li v-for="song in songs">
          <p>{{ song.title }}</p>
          <p>{{ song.artist }}</p>
          <img :src="song.src" alt="">
          <audio  controls>
            <source :src="song.music" type="audio/mpeg" />
          </audio> -->
        <!-- </li> -->
      <!-- </ul> -->
    </div>
   </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      current:{},
      index:0,
      isPlaying:false,  
      songs:[
        { title:"Grateful",
          artist:'Neffex',
          src:require("./assets/song1.jpg"),
          music:require("./assets/day15.mp3")
        },
        {title:"Hand Of God",
          artist:'Jimi',
          src:require("./assets/song3.jpg"),
          music:require("./assets/fresh19.mp3")
        },
        {title:"Lecture",
          artist:'ISiak Abolore',
          src:require("./assets/song3.jpg"),
          music:require("./lecture/lecture.mp3")
        },
        {title:"Ipe Ododo",
          artist:'Isiak Abolore',
          src:require("./assets/song3.jpg"),
          music:require("./lecture/IPEODODO.mp3")
        },
        {title:"Ramadan Day 14",
          artist:'Abolore Radio programm',
          src:require("./assets/song3.jpg"),
          music:require("./lecture/day14.mp3")
        },
        {title:"Ramadan Day 10",
          artist:'Isiak Radio programm',
          src:require("./assets/song3.jpg"),
          music:require("./lecture/day10.mp3")
        },
      ],
      player: new Audio()

    }
  },
  created(){
this.current = this.songs[this.index];
this.player.src =this.current.music;
// this.player.play()
  },
  methods:{
    play(song){
      if(typeof song.music != 'undefined'){
        this.current = song;

        this.player.src = this.current.music;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause(){
      this.player.pause();
      this.isPlaying = false;
    },
    prev(){
      this.index--;
      if(this.index < 0 ){
        this.index = this.songs.length - 1
      }

      this.current = this.songs[this.index]
      this.play(this.current)

    },
    next(){
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0
      }

      this.current = this.songs[this.index]
      this.play(this.current)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

main{
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title{
  color:#53565A ;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span{
  font-weight: 400;
  font-style: italic;
}
.controls{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button{
  appearance: none;
  background:none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover{
  opacity: 0.8;
} 
.play, .pause{
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background: #CC2E5D;
}
.next, .prev{
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background: #FF5858;
}

.playlist{
padding: 0px 30px;
}

.playlist h3{
  color:#212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song{
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .song:hover{
  color: #FF5858;
}
.playlist .song.playing{
  color: #fff;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
