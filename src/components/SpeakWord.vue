<template>
  <!-- Container for the audio player and control button -->
  <div class="audio-and-control">
    <!-- Play/Pause button with dynamic class binding based on playing state -->
    <div
      class="big-button"
      :class="{ playing: playing }"
      @click="togglePlayPause"
    >
      <!-- Play icon, shown when audio is not playing -->
      <div class="play-icon" v-show="!playing"></div>
      <!-- Pause icon, shown when audio is playing -->
      <div class="pause-icon" v-show="playing"></div>
    </div>
    <!-- Audio element with reactive source binding -->
    <audio ref="wordPlayer" :src="url" @ended="stop"></audio>
  </div>
</template>

<script>
export default {
  props: {
    url: String, // Expect a string URL for the audio source
  },
  data() {
    return {
      playing: false, // State to track if the audio is currently playing
    };
  },
  methods: {
    stop() {
      this.playing = false; // Set playing to false when audio ends
    },
    togglePlayPause() {
      const player = this.$refs.wordPlayer; // Reference to the audio element
      if (player) {
        if (!this.playing) {
          player.play(); // Play the audio if not currently playing
        } else {
          player.pause(); // Pause the audio if currently playing
        }
        this.playing = !this.playing; // Toggle the playing state
      }
    },
  },
  mounted() {
    // Event listener for 'ended' event is now handled in the template with @ended
  },
};
</script>

<style>
/* Styles omitted for brevity */
</style>
