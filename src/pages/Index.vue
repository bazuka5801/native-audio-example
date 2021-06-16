<template>
  <q-page class="flex column flex-center">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    >
    <div>{{ currentTime }} / {{ duration }}</div>
    <q-btn label="preload" @click="preload" />
    <q-btn label="play" @click="play" />
    <q-btn label="playEnd" @click="playEnd" />
    <q-btn label="pause" @click="pause" />
    <q-btn label="resume" @click="resume" />
    <q-btn label="stop" @click="stop" />
    <q-btn label="loop" @click="loop" />
    <q-btn label="setVolume" @click="setVolume" />
    <q-btn label="unload" @click="unload" />
    <q-btn label="getCurrentTime" @click="getCurrentTime" />
    <q-btn label="getDuration" @click="getDuration" />
  </q-page>
</template>

<script>
import {NativeAudio} from '@capacitor-community/native-audio'
export default {
  name: 'PageIndex',
  data: () => ({
    duration: null,
    currentTime: null
  }),
  mounted() {
    setInterval(() => {
      this.getCurrentTime()
      this.getDuration()
    }, 100)
  },
  methods: {
    preload() {
      NativeAudio.preload({
        assetId: "fire",
        assetPath: "fire.mp3"
      })
    },
    play() {
      NativeAudio.play({
        assetId: "fire"
      })
    },
    playEnd() {
      NativeAudio.play({
        assetId: "fire",
        time: 198.0
      })
    },
    pause() {
      NativeAudio.pause({
        assetId: "fire"
      })
    },
    resume() {
      NativeAudio.resume({
        assetId: "fire"
      })
    },
    stop() {
      NativeAudio.stop({
        assetId: "fire"
      })
    },
    loop() {
      NativeAudio.loop({
        assetId: "fire"
      })
    },
    setVolume() {
      NativeAudio.setVolume({
        assetId: "fire",
        volume: Math.random()
      })
    },
    unload() {
      NativeAudio.unload({
        assetId: "fire"
      })
    },
    async getCurrentTime() {
      this.currentTime = (await NativeAudio.getCurrentTime({
        assetId: "fire"
      })).currentTime.toFixed(1)
    },
    async getDuration() {
      this.duration = (await NativeAudio.getDuration({
        assetId: "fire"
      })).duration.toFixed(1)
    },
  }
}
</script>
