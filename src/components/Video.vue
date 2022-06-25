<template>
  <div>
    <button v-if="!isPlaying" @click="play">Play</button>
    <hr />
    <div id="player" data-vimeo-id="162391385" class="vlite-js"></div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
import Vlitejs from "vlitejs";
import VlitejsVimeo from "vlitejs/dist/providers/vimeo";

Vlitejs.registerProvider("vimeo", VlitejsVimeo);

export default {
  name: "v-video",
  setup() {
    const isPlaying = ref(false);
    const playerInstance = ref();

    const play = () => {
      isPlaying.value = true;
      playerInstance.value.player.play();
    };

    const options = {
      controls: true,
      autoplay: false,
      playPause: true,
      progressBar: true,
      time: true,
      volume: true,
      fullscreen: true,
      bigPlay: true,
      playsinline: true,
      loop: true,
      muted: false,
      autoHide: true,
      providerParams: {},
    };

    onMounted(() => {
      playerInstance.value = new Vlitejs("#player", {
        options: {
          ...options,
        },
        provider: "vimeo",
      });
    });

    return {
      play,
      isPlaying,
    };
  },
};
</script>

<style lang="scss">
@import "vlitejs/dist/vlite.css";
</style>
