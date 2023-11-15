<template>
  <div class="container">
    <div class="flex-container">
      <AudioPlayer ref="audioPlayer" :option="currentTrack" class="audio-player"/>
      <div class="track-list">
        <Track v-for="(track, index) in trackList" :track="track" :key="index" 
              :is-play="track.title === currentTrack.title && !!audioPlayer && audioPlayer.isPlaying"
              @play="handlePlay(track)"
              @pause="audioPlayer?.pause()"
              @click-on-track="handleClickOnTrack(track)"
              :class="(track.title === currentTrack.title && !!audioPlayer && audioPlayer.isPlaying) ? 'bg-current-track' : ''"
              />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import AudioPlayer from 'vue3-audio-player'
import 'vue3-audio-player/dist/style.css'
import type { TrackInterface } from '~/types/TrackInterface';
import Track from '~/components/Track.vue';

const trackList: TrackInterface[] = [
  { title: '1 track', author: 'Author1', duration: '2:43', coverImage: '/track-images/1.webp', src: '/music.mp3' },
  { title: '2 track', author: 'Author2', duration: '2:43', coverImage: '/track-images/2.webp', src: '/music.mp3' },
  { title: '3 track', author: 'Author3', duration: '2:43', coverImage: '/track-images/3.webp', src: '/music.mp3' },
  { title: '4 track', author: 'Author4', duration: '2:43', coverImage: '/track-images/4.webp', src: '/music.mp3' },
  { title: '5 track', author: 'Author5', duration: '2:43', coverImage: '/track-images/5.webp', src: '/music.mp3' },
  { title: '6 track', author: 'Author6', duration: '2:43', coverImage: '/track-images/6.webp', src: '/music.mp3' },
  { title: '7 track', author: 'Author7', duration: '2:43', coverImage: '/track-images/7.webp', src: '/music.mp3' },
  { title: '8 track', author: 'Author8', duration: '2:43', coverImage: '/track-images/8.webp', src: '/music.mp3' },
  { title: '9 track', author: 'Author9', duration: '2:43', coverImage: '/track-images/9.webp', src: '/music.mp3' },
  { title: '10 track', author: 'Author10', duration: '2:43', coverImage: '/track-images/10.webp', src: '/music.mp3' },
  { title: '11 track', author: 'Author11', duration: '2:43', coverImage: '/track-images/11.webp', src: '/music.mp3' },
  { title: '12 track', author: 'Author12', duration: '2:43', coverImage: '/track-images/12.webp', src: '/music.mp3' },
  { title: '13 track', author: 'Author13', duration: '2:43', coverImage: '/track-images/13.webp', src: '/music.mp3' },
  { title: '14 track', author: 'Author14', duration: '2:43', coverImage: '/track-images/14.webp', src: '/music.mp3' },
  { title: '15 track', author: 'Author15', duration: '2:43', coverImage: '/track-images/15.webp', src: '/music.mp3' },
  { title: '16 track', author: 'Author16', duration: '2:43', coverImage: '/track-images/16.webp', src: '/music.mp3' },
  { title: '17 track', author: 'Author17', duration: '2:43', coverImage: '/track-images/17.webp', src: '/music.mp3' },
  { title: '18 track', author: 'Author18', duration: '2:43', coverImage: '/track-images/18.webp', src: '/music.mp3' },
  { title: '19 track', author: 'Author19', duration: '2:43', coverImage: '/track-images/19.webp', src: '/music.mp3' },
]

const currentTrack = ref<TrackInterface>(trackList[0])
const audioPlayer = ref<InstanceType<typeof AudioPlayer> | null>(null)

function handlePlay(track: TrackInterface) {
  if(currentTrack.value.title !== track.title) {
    currentTrack.value = track
  }
  audioPlayer.value?.play()
}

function handleClickOnTrack(track: TrackInterface) {
  if(!!audioPlayer.value && audioPlayer.value.isPlaying && currentTrack.value.title === track.title) {
     audioPlayer.value.pause()
  } else if(!!audioPlayer.value) {
    handlePlay(track)
  }
}

</script>

<style scoped lang="scss">
.container {
  height: 100vh;
  display: flex;
  align-items: center;
  padding: 20px;
  box-sizing: border-box;
  padding-top: 74px;
  @media (max-height: 820px) {
    height: 100%;
    padding-top: 30px;
  }
}

.flex-container {
  width: 100%;
  display: flex;
  background-color: white;
  border-radius: 16px;
  padding: 20px;
  border: 1px solid #c4c4c4;
  div {
    flex-grow: 1;
  }

  @media (max-width: 1024px) or (max-height: 820px) {
    flex-direction: column;
  }
}

.track-list {
  max-height: 80vh;
  max-width: 60%;
  overflow-y: hidden;
  box-sizing: border-box;
  scrollbar-gutter: stable;
  &:hover {
    overflow-y: auto;
  }

  @media (max-width: 1024px) {
    max-width: 100%;
    max-height: 60vh;
  }

  @media (max-height: 820px) {
    max-width: 100%;
    max-height: 100%;
  }
}

.audio-player {
  align-self: center;
  padding-bottom: 30px;
  @media (max-width: 1023px) {
    width: 100%;
  }
}
.bg-current-track {
  background-color: #f0f0f0;
}
</style>