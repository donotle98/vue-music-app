<template>
  <div id="app">
    <main>
      <section class="player">
        <div class="song-info">
          <img class="album-cover" v-bind:src="current.img"/>
          <h2 class="song-album">{{current.album}}</h2>
          <h2 class="song-title">{{current.title}} - <span>{{current.artist}}</span></h2>
        </div>
        <div class="controls">
          <button class="prev" @click="prev"><font-awesome-icon icon="backward"/></button>
          <button class="play" v-if="!isPlaying" @click="play"><font-awesome-icon icon="play"/></button>
          <button class="pause" v-else @click="pause"><font-awesome-icon icon="pause"/></button>
          <button class="next" @click="next"><font-awesome-icon icon="forward"/></button>
        </div>
      </section>
      <div class="playlist">
        <div :class="(song.src == current.src) ? 'each-song playing' : 'each-song'" v-for="song in songs" :key='song.src'>
            <img v-bind:src="song.img"/>
            <button  @click="play(song)" >{{song.title}} - {{song.artist}}</button>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function () {
    return {
      current: {
      },
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Problemz',
          album: 'Escape From New York',
          artist: 'Beast Coast',
          src: require('./assets/03 Problemz (feat. Erick the Architect, CJ Fly, The Underachievers, Zombie Juice & Nyck Caution).mp3'),
          img: require('./assets/efny_cover.png')
        },
        {
          title: 'Far Away',
          album: 'Escape From New York',
          artist: 'Beast Coast',
          src: require('./assets/04 Far Away (feat. Kirk Knight, Meechy Darko, Erick the Architect, Nyck Caution & Joey Bada$$).mp3'),
          img: require('./assets/efny_cover.png')
        },
        {
          title: 'One More Round',
          album: 'Escape From New York',
          artist: 'Beast Coast',
          src: require('./assets/11 One More Round (feat. Meechy Darko, Erick the Architect, Nyck Caution & Joey Bada$$).mp3'),
          img: require('./assets/efny_cover.png')
        },
        {
          title: 'Coast Clear',
          album: 'Escape From New York',
          artist: 'Beast Coast',
          src: require('./assets/12 Coast_Clear (feat. Joey Bada$$, Flatbush Zombies, Kirk Knight, Nyck Caution & Issa Gold).mp3'),
          img: require('./assets/efny_cover.png')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play (song) {
      if(typeof song.src != 'undefined'){
        this.current = song;

        this.player.src = this.current.src;
      }

      this.player.play();
      this.isPlaying = true;
    },
    pause(){
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
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
}

</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body{
  font-family: sans-serif;
  background-color: black;
}

.song-info{
  color: white;
  text-align: center;
  margin-top: 2rem;
  margin-bottom: 2rem;
}

.song-album{
  margin-bottom: 2rem;
  font-size: 1.1rem;
}

.album-cover{
  margin-bottom: 1.5rem;
  -webkit-animation: boxColor 20s infinite;
  animation: boxColor 10s infinite;
  -webkit-animation-direction: alternate;
  animation-direction: alternate;
  border-radius: 4rem;
}

.controls{
  text-align: center;
  display: flex;
  justify-content: space-around;
}

.controls button{
  padding: .5rem .75rem;
  color: white;
  font-size: 1.9rem;
  border: none;
  background: transparent;
}

button:focus{
  outline: none;
}

.playlist{
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 3rem;
  padding-top: 3rem;
}

.playlist img{
  width: 3rem;
  height: 3rem;
  margin-left: 2rem;
}

.playlist button{
  color: white;
  width: 20rem;
  border: none;
  background: transparent;
  font-size: 1.2rem;
  text-align: left;
  margin-left: 1rem;
}

.each-song{
  display: flex;
  margin-bottom: 2rem;
  transition: .5s;
}

.playing{
  -webkit-animation: boxColor 20s infinite;
  animation: boxColor 10s infinite;
  -webkit-animation-direction: alternate;
  animation-direction: alternate;
  padding-top: .5rem;
  padding-bottom: .5rem;
  transition: .5s;
}

@keyframes boxColor {
  0% {
        box-shadow: 0px 0px 40px #45a3e5;
    }

    30% {
        box-shadow: 0px 0px 40px #66bf39
    }

    60% {
        box-shadow: 0px 0px 40px #eb670f
    }

    90% {
        box-shadow: 0px 0px 40px #f35
    }

    100% {
        box-shadow: 0px 0px 40px #864cbf
    }
}
</style>
