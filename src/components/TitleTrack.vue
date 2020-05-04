<template>
<div class="sc-player__title">
  <Wave :percent-played="percentPlayed" />

  <a class="sc-link-title" :href="permalink" target="_blank" rel="noopener noreferrer">
    <marquee-text :repeat="3">

      <span> {{ title }}</span>
    </marquee-text>
  </a>
</div>
</template>

<script>
import MarqueeText from 'vue-marquee-text-component'
import Wave from './Wave.vue';

export default {
  name: "TitleTrack",
  components: {
    MarqueeText,
    Wave
  },
  props: {
    permalink: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: ''
    },
    percentPlayed: {
      type: Number,
      default: 0
    }
  }
};
</script>
<style scoped>
.sc-link-title .marquee-text-text {
  margin-left: 1em;
}
</style>
