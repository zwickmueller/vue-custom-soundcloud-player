<template>
<div class="sifi tag sc-button" @click="nextTrack">

  <svg width="33" height="23" viewBox="0 0 33 23" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path fill-rule="evenodd" clip-rule="evenodd" d="M12.5742 8.54425V14.4558L16.9707 11.999V14.4558L21.2798 11.3358L16.9707 8.54425V10.7425L12.5742 8.54425Z" fill="rgba(236, 236, 236,.5)" />
    <path
      d="M12.5742 14.4558H12.0742V15.3079L12.8181 14.8922L12.5742 14.4558ZM12.5742 8.54425L12.7978 8.09704L12.0742 7.73524V8.54425H12.5742ZM16.9707 11.999H17.4707V11.1468L16.7268 11.5625L16.9707 11.999ZM16.9707 14.4558H16.4707V15.4351L17.2639 14.8608L16.9707 14.4558ZM21.2798 11.3358L21.573 11.7408L22.164 11.3129L21.5516 10.9162L21.2798 11.3358ZM16.9707 8.54425L17.2426 8.12461L16.4707 7.62458V8.54425H16.9707ZM16.9707 10.7425L16.7471 11.1897L17.4707 11.5515V10.7425H16.9707ZM13.0742 14.4558V8.54425H12.0742V14.4558H13.0742ZM16.7268 11.5625L12.3303 14.0193L12.8181 14.8922L17.2146 12.4354L16.7268 11.5625ZM17.4707 14.4558V11.999H16.4707V14.4558H17.4707ZM20.9865 10.9308L16.6775 14.0508L17.2639 14.8608L21.573 11.7408L20.9865 10.9308ZM16.6988 8.96389L21.0079 11.7555L21.5516 10.9162L17.2426 8.12461L16.6988 8.96389ZM17.4707 10.7425V8.54425H16.4707V10.7425H17.4707ZM12.3506 8.99147L16.7471 11.1897L17.1943 10.2952L12.7978 8.09704L12.3506 8.99147Z"
      fill="rgba(236, 236, 236,.5)" />
  </svg>


</div>
<!-- <button class="sc-player__next" type="button" @click="nextTrack" /> -->
</template>

<script>
export default {
  name: "NextButton",
  props: {
    setCurrentTrack: {
      type: Function,
      default: undefined
    },
    soundcloud: {
      type: Object,
      default: undefined
    },
    sounds: {
      type: Array,
      default: () => {
        return [];
      }
    },
    trackIndex: {
      type: Number,
      default: 0
    }
  },
  methods: {
    nextTrack() {
      this.soundcloud.isPaused((paused) => {
        if (paused) {
          console.log(this.soundcloud);
          this.soundcloud.next().pause();
        } else {
          this.soundcloud.next();
        }
      });
      this.setCurrentTrack(
        this.sounds[this.trackIndex + 1],
        this.trackIndex + 1
      );
    }
  }
};
</script>
