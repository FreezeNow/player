<template>
  <div class="home-box">
    <home-header />
    <div class="music-box">
      <ul class="music-list">
        <li
          class="music"
          v-for="(music, index) of musicList"
          :key="music.name"
          @click="musicClick(music, index)"
        >{{ music.name }}</li>
      </ul>
      <div
        class="music-play"
        :class="{play}"
        :style="{
          top: 40 * (music.index + 1) + 'px'
        }"
      >
        <span></span>
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
    <div>
      <audio
        controls
        :src="require(`D:/as/${music.src}`)"
        volume="1"
        @ended="musicEnded"
        @playing="musicPlaying"
        @pause="musicPause"
        @canplay="musicCanplay"
      >
        Your browser does not support the
        <code>audio</code> element.
      </audio>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import homeHeader from '@/components/home-header.vue';

export default {
  name: 'Home',
  data() {
    return {
      play: false,
      musicList: [
        // { name: '',}
      ],
      music: {
        index: 0,
        name: '',
        src: '',
      },
    };
  },
  methods: {
    musicClick(music, index) {
      this.music.index = index;
      this.music.name = this.musicList[index].name;
      this.music.src = this.musicList[index].src;
      // this.musicPause();
      // document.querySelector('audio').play();
    },
    musicPause() {
      this.play = false;
    },
    musicPlaying() {
      this.play = true;
    },
    getMusicList() {
      this.musicList = [
        {
          name: 'ASIAN KUNG-FU GENERATION - Re：Re： (Single ver.)',
          src: 'ASIAN KUNG-FU GENERATION - Re：Re： (Single ver.).mp3',
        },
        {
          name: 'George Winston - Variations on the Kanon By Pachelbel',
          src: 'George Winston - Variations on the Kanon By Pachelbel.mp3',
        },
      ];
      this.music.index = 0;
      this.music.name = this.musicList[this.music.index].name;
      this.music.src = this.musicList[this.music.index].src;
    },
    musicEnded() {
      if (this.music.index + 1 < this.musicList.length) {
        this.music.index += 1;
      } else {
        this.music.index = 0;
      }
      this.music.src = this.musicList[this.music.index];
    },
    musicCanplay() {
      this.musicPause();
    },
  },
  created() {
    this.getMusicList();
  },
  components: {
    homeHeader,
  },
};
</script>
<style lang="stylus" scoped>
@keyframes music-play {
  0% {
    height: 50%;
  }

  100% {
    height: 100%;
  }
}

.home-box {
}

.music-box {
  margin-bottom: height-base;
}

.music {
  box-sizing: border-box;
  padding-left: padding-base;
  padding-right: width-base;
  height: height-base;
  line-height: height-base;
  border-bottom: 1px solid color-border;
  text-align: left;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.music-play {
  display: flex;
  margin: 10px auto;
  width: 10px;
  height: 20px;
  justify-content: space-around;
  align-items: center;
  position: fixed;
  right: 10px;

  span {
    display: block;
    width: 1.5px;
    height: 100%;
    background-color: color-theme;
    position: relative;
    bottom: 0;

    &:nth-child(1) {
      height: 70%;
    }

    &:nth-child(2) {
      height: 50%;
    }

    &:nth-child(3) {
      height: 80%;
    }

    &:nth-child(4) {
      height: 50%;
    }
  }

  &.play {
    span {
      animation: music-play linear infinite alternate 0.3s;

      &:nth-child(2) {
        animation-delay: 0.15s;
      }

      &:nth-child(3) {
        animation-delay: 0.075s;
      }

      &:nth-child(4) {
        animation-delay: 0.2s;
      }
    }
  }
}

audio {
  width: 100%;
  height: height-base;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
}
</style>
