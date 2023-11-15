<template>
  <div class="track" @click="$emit('click-on-track')">
    <div class="flex-container">
      <NuxtImg class="track-image" :src="props.track.coverImage" :alt="props.track.title" />
      <div>
        <div style="padding-bottom: 5px;">
          {{ props.track.title }}
        </div>
        <div v-if="width < 1280" style="color: #a6a6a6;">
          {{ props.track.author }}
        </div>
      </div>
    </div>
    <div v-if="width > 1279">
      {{ props.track.author }}
    </div>
    <div style="justify-self: center;">
      {{ props.track.duration }}
    </div>
    <div v-if="width > 479" style="justify-self: center;">
      <Transition mode="out-in">
        <button v-if="!props.isPlay" @click.stop="$emit('play')">
          <NuxtImg src="/play-button.svg" alt="Play" />
        </button>
        <button @click.stop="$emit('pause')" v-else>
          <NuxtImg src="/pause-button.svg" alt="Pause" />
        </button>
      </Transition>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { TrackInterface } from '~/types/TrackInterface';

const props = defineProps<{ track: TrackInterface, isPlay: boolean, }>()

const { width } = useWindowSize()
</script>

<style scoped lang="scss">
.track {
  display: grid;
  grid-template-columns: 2fr 2fr 1fr 1fr;
  align-items: center;
  color: #a6a6a6;
  padding: 5px 10px;
  border-bottom: 1px solid #a6a6a6;
  transition: all 0.3s;

  &:hover {
    cursor: pointer;
    background-color: #f0f0f0;
  }

  @media (max-width: 1279px) {
    grid-template-columns: 2fr 1fr 1fr;
  }

  @media (max-width: 479px) {
    grid-template-columns: 2fr 1fr;
  }
}

.track-image {
  width: 40px;
  height: 40px;
}

.flex-container {
  display: flex;
  column-gap: 10px;
  align-items: center;
  color: black;
  min-width: 0;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}

button {
  display: inline-block;

  img {
    height: 20px;
    width: 20px;
    transition: transform 0.3s;

    &:hover {
      transform: scale(1.2);
    }
  }
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>