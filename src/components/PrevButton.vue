<template>
<!-- <button class="sc-player__prev" type="button" @click="prevTrack" /> -->

<div class="sifi tag sc-button" @click="prevTrack">


  <svg width="33" height="23" viewBox="0 0 33 23" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path fill-rule="evenodd" clip-rule="evenodd" d="M20.8872 14.4558L20.8872 8.54425L16.4907 11.0011V8.54425L12.1816 11.6642L16.4907 14.4558V12.2575L20.8872 14.4558Z" fill="rgba(236, 236, 236,.5)" />
    <path
      d="M20.8872 8.54425L21.3872 8.54425L21.3872 7.69207L20.6433 8.10778L20.8872 8.54425ZM20.8872 14.4558L20.6636 14.903L21.3872 15.2648L21.3872 14.4558L20.8872 14.4558ZM16.4907 11.0011H15.9907V11.8532L16.7346 11.4375L16.4907 11.0011ZM16.4907 8.54425H16.9907V7.56493L16.1975 8.13926L16.4907 8.54425ZM12.1816 11.6642L11.8884 11.2592L11.2974 11.6871L11.9098 12.0838L12.1816 11.6642ZM16.4907 14.4558L16.2188 14.8754L16.9907 15.3754V14.4558H16.4907ZM16.4907 12.2575L16.7143 11.8103L15.9907 11.4485V12.2575H16.4907ZM20.3872 8.54425L20.3872 14.4558L21.3872 14.4558L21.3872 8.54425L20.3872 8.54425ZM16.7346 11.4375L21.1311 8.98072L20.6433 8.10778L16.2468 10.5646L16.7346 11.4375ZM15.9907 8.54425V11.0011H16.9907V8.54425H15.9907ZM12.4749 12.0692L16.7839 8.94924L16.1975 8.13926L11.8884 11.2592L12.4749 12.0692ZM16.7626 14.0361L12.4535 11.2446L11.9098 12.0838L16.2188 14.8754L16.7626 14.0361ZM15.9907 12.2575V14.4558H16.9907V12.2575H15.9907ZM21.1108 14.0085L16.7143 11.8103L16.2671 12.7048L20.6636 14.903L21.1108 14.0085Z"
      fill="rgba(236, 236, 236,.5)" />
  </svg>

</div>
</template>

<script>
export default {
  name: "PrevButton",
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
    prevTrack() {
      this.soundcloud.isPaused((paused) => {
        if (paused) {
          this.soundcloud.prev().pause();
        } else {
          this.soundcloud.prev();
        }
      });
      this.setCurrentTrack(
        this.sounds[this.trackIndex - 1],
        this.trackIndex - 1
      );
    }
  }
};
</script>
