<template>
<div class="sc-player__artist is-narrow sifi tag">
  <a class="sc-link-artist" :href="artistUrl" target="_blank" rel="noopener noreferrer">
  </a>
</div>
</template>

<script>
export default {
  name: "TitleArtist",

  props: {
    artist: {
      type: String,
      default: ''
    },
    artistUrl: {
      type: String,
      default: ''
    }
  }
};
</script>
