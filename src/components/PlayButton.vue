<template>
<!-- <button :class="buttonClasses" type="button" @click="playPause" /> -->

<div class="sifi tag sc-button" @click="playPause">
  <svg v-if="isPaused" width="32" height="23" viewBox="0 0 32 23" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path d="M12.1846 17.4085V6.45581L22.529 11.6279L12.1846 17.4085Z" fill="rgba(236, 236, 236,.75)" />
  </svg>

  <svg v-else width="32" height="23" viewBox="0 0 32 23" fill="none" xmlns="http://www.w3.org/2000/svg">
    <rect x="11.5273" y="6.28391" width="3.30342" height="10.4322" fill="rgba(236, 236, 236,.75)" />
    <rect x="17.1689" y="6.28391" width="3.30342" height="10.4322" fill="rgba(236, 236, 236,.75)" />
  </svg>

</div>
</template>

<script>
import classnames from 'classnames';

export default {
  name: "PlayButton",
  data() {
    return {
      isPaused: true
    }
  },
  props: {
    soundcloud: {
      type: Object,
      default: undefined
    },
    trackPlaying: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    buttonClasses() {
      return classnames('sc-player__play', {
        'sc-player--pause': this.trackPlaying
      });
    }
  },
  methods: {
    playPause() {
      this.soundcloud.isPaused((paused) => {
        if (paused) {
          this.isPaused = false;
          this.soundcloud.play();
        } else {
          this.isPaused = true;
          this.soundcloud.pause();
        }
      });
    }
  }
};
</script>
