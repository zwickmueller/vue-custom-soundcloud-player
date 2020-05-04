<template>
<div class="sc-player__title">
  <a class="sc-link-title" :href="permalink" target="_blank" rel="noopener noreferrer">
    <marquee-text :repeat="3">

      <span> {{ title }}</span>
    </marquee-text>
  </a>
</div>
</template>

<script>
import MarqueeText from 'vue-marquee-text-component'

export default {
  name: "TitleTrack",
  components: {
    MarqueeText
  },
  props: {
    permalink: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: ''
    }
  }
};
</script>
<style scoped>
.sc-link-title .marquee-text-text {
  margin-left: 1em;
}
</style>
