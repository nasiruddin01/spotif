<template>
  <div class="container" id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} - <span>{{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">
            <svg
              height="24"
              width="30"
              aria-hidden="true"
              focusable="false"
              data-prefix="fal"
              data-icon="backward"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 512 512"
              class="svg-inline--fa fa-backward fa-w-16 fa-2x"
            >
              <path
                fill="currentColor"
                d="M267.5 281.1l192 159.4c20.6 17.2 52.5 2.8 52.5-24.6V96c0-27.4-31.9-41.8-52.5-24.6L267.5 232c-15.3 12.8-15.3 36.4 0 49.1zm20.5-24.5L480 96v320L288 256.6zM11.5 281.1l192 159.4c20.6 17.2 52.5 2.8 52.5-24.6V96c0-27.4-31.9-41.8-52.5-24.6L11.5 232c-15.3 12.8-15.3 36.4 0 49.1zM32 256.6L224 96v320L32 256.6z"
                class=""
              ></path>
            </svg>
          </button>

          <button class="play" v-if="!isPlaying" @click="play">
            <svg
              height="24"
              width="30"
              aria-hidden="true"
              focusable="false"
              data-prefix="fal"
              data-icon="play"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 448 512"
              class="svg-inline--fa fa-play fa-w-14 fa-2x"
            >
              <path
                fill="currentColor"
                d="M424.4 214.7L72.4 6.6C43.8-10.3 0 6.1 0 47.9V464c0 37.5 40.7 60.1 72.4 41.3l352-208c31.4-18.5 31.5-64.1 0-82.6zm-16.2 55.1l-352 208C45.6 483.9 32 476.6 32 464V47.9c0-16.3 16.4-18.4 24.1-13.8l352 208.1c10.5 6.2 10.5 21.4.1 27.6z"
                class=""
              ></path>
            </svg>
          </button>

          <button class="pause" v-else @click="pause">
            <svg
              height="24"
              width="30"
              aria-hidden="true"
              focusable="false"
              data-prefix="fal"
              data-icon="pause"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 448 512"
              class="svg-inline--fa fa-pause fa-w-14 fa-3x"
            >
              <path
                fill="currentColor"
                d="M48 479h96c26.5 0 48-21.5 48-48V79c0-26.5-21.5-48-48-48H48C21.5 31 0 52.5 0 79v352c0 26.5 21.5 48 48 48zM32 79c0-8.8 7.2-16 16-16h96c8.8 0 16 7.2 16 16v352c0 8.8-7.2 16-16 16H48c-8.8 0-16-7.2-16-16V79zm272 400h96c26.5 0 48-21.5 48-48V79c0-26.5-21.5-48-48-48h-96c-26.5 0-48 21.5-48 48v352c0 26.5 21.5 48 48 48zM288 79c0-8.8 7.2-16 16-16h96c8.8 0 16 7.2 16 16v352c0 8.8-7.2 16-16 16h-96c-8.8 0-16-7.2-16-16V79z"
                class=""
              ></path>
            </svg>
          </button>

          <button class="next" @click="next">
            <svg
              height="24"
              width="30"
              aria-hidden="true"
              focusable="false"
              data-prefix="fal"
              data-icon="forward"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 512 512"
              class="svg-inline--fa fa-forward fa-w-16 fa-2x"
            >
              <path
                fill="currentColor"
                d="M244.5 230.9L52.5 71.4C31.9 54.3 0 68.6 0 96v320c0 27.4 31.9 41.8 52.5 24.6l192-160.5c15.3-12.9 15.3-36.5 0-49.2zM224 255.4L32 416V96l192 159.4zm276.5-24.5l-192-159.4C287.9 54.3 256 68.6 256 96v320c0 27.4 31.9 41.8 52.5 24.6l192-160.5c15.3-12.9 15.3-36.5 0-49.2zM480 255.4L288 416V96l192 159.4z"
                class=""
              ></path>
            </svg>
          </button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="{ playing: song.isPlaying }"
        >
          {{ song.title }} -{{ song.artist }}
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
          title: "Jodi mon kade",
          artist: "Shawon",
          src: require("./assets/jodi-mon.mp3"),
          isPlaying: false
        },
        {
          title: "Kisu kisu number",
          artist: "Unknown",
          src: require("./assets/kisu-kisu.mp3"),
          isPlaying: false
        }
      ],
      player: new Audio()
    };
  },
  methods: {
    play(song) {
      if (typeof song.src !== "undefined") {
        this.current = song;
        this.player.src = this.current.src;
        this.isPlaying = true;
      }
      this.isPlaying = true;
      this.songs[this.index].isPlaying = true;
      this.player.play();
      this.player.addEventListener(
        "ended",
        function() {
          this.index++;
          if (this.index > this.songs.length - 1) {
            this.index = 0;
          }
          this.current = this.songs[this.index];
          this.play(this.current);
        }.bind(this)
      );
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
      this.songs[this.index].isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700&family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600&display=swap");

$bg-primary: #c3aed6;
$bg-secondary: #efbbcf;
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Montserrat", sans-serif;
  max-width: 768px;
  margin: auto;
  .container {
    background-color: $bg-primary;
    box-shadow: 14px 10px 14px -7px #393b44;
    border-radius: 5px;

    header {
      display: flex;
      justify-content: center;
      align-items: center;
      margin-top: 2rem;
      padding: 15px;
      border-radius: 5px 5px 0px 0px;
      background-color: $bg-secondary;
      color: #fff;
    }
    main {
      width: 100%;
      margin: 0 auto;
      .song-title {
        text-align: center;
        margin: 1rem 0;
      }
      .controls {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        button {
          margin: 0.5rem;
          border: none;
          color: #cffffe;
          background-color: $bg-primary;
        }
        .prev {
          outline: none;
        }
        .play {
          outline: none;
        }
        .pause {
          outline: none;
        }
        .next {
          outline: none;
        }
      }
      .playlist {
        text-align: center;
        h3 {
          margin: 2rem 0;
        }
        button {
          border: none;
          background-color: $bg-primary;
          margin: 1rem;
          font-family: "Lato", sans-serif;
          font-size: 1rem;
          outline: none;
        }
        .song {
          color: #000;
          outline: none;
        }
        .playing {
          color: #cffffe;
          outline: none;
        }
      }
    }
  }
}
</style>
