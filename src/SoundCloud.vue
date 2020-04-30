<template>
<div class="sc-player">
  <div v-if="currentTrack" :class="currentTrackClasses">
    <Buttons :set-current-track="setCurrentTrack" :soundcloud="soundcloud" :sounds="sounds" :track-index="trackIndex" :track-playing="trackPlaying" />
    <TitleTrack :permalink="currentTrack.permalink_url" :title="currentTrack.title" />
    <TitleArtist :artist="currentTrack.artist" :artist-url="currentTrack.artist_url" />
    <Wave :percent-played="percentPlayed" />
  </div>
  <Playlist :set-current-track="setCurrentTrack" :soundcloud="soundcloud" :sounds="sounds" :theme="theme" />
  <Iframe :playlist="playlist" :track="track" @setIframeRef="onSetIframeRef" />
</div>
</template>

<script>
// const soundcloudApi = 'https://w.soundcloud.com/player/api.js';
import classnames from "classnames";
import {
  soundcloudApi
} from "./utils/consts";
import loadScript from "./utils/loadScript";
import Buttons from './components/Buttons.vue';
import Iframe from './components/Iframe.vue';
import Playlist from './components/Playlist.vue';
import TitleArtist from './components/TitleArtist.vue';
import TitleTrack from './components/TitleTrack.vue';
import Wave from './components/Wave.vue';
import './SoundCloud.css'

export default {
  name: 'SoundCloud',
  components: {
    Buttons,
    Iframe,
    Playlist,
    TitleArtist,
    TitleTrack,
    Wave
  },
  props: {
    mini: {
      type: Boolean,
      default: false
    },
    playlist: {
      type: String,
      default: undefined
    },
    theme: {
      type: String,
      default: "dark"
    },
    track: {
      type: String,
      default: undefined
    }
  },
  data() {
    return {
      currentTrack: null,
      iframeRef: null,
      percentPlayed: 0,
      soundcloud: null,
      sounds: [],
      trackIndex: 0,
      trackPlaying: false
    }
  },
  computed: {
    currentTrackClasses() {
      return classnames('sc-player__current', {
        'sc-player--mini': this.mini
      });
    }
  },
  methods: {
    bindSoundcloudEvents() {
      const component = this;
      this.soundcloud.bind('ready', () => {
        component.soundcloud.getSounds((sounds) => {
          const tracks = sounds.filter(sound => sound.hasOwnProperty('title'));
          component.sounds = tracks;
          component.setCurrentTrack(tracks[0], 0);
        });
      });
      // eslint-disable-next-line no-undef
      this.soundcloud.bind(SC.Widget.Events.PAUSE, () => {
        component.trackPlaying = false;
      });
      // eslint-disable-next-line no-undef
      this.soundcloud.bind(SC.Widget.Events.PLAY, () => {
        component.trackPlaying = true;
      });
      // eslint-disable-next-line no-undef
      this.soundcloud.bind(SC.Widget.Events.PLAY_PROGRESS, function(progress) {
        const position = Number(((progress.currentPosition / component.currentTrack.duration) * 100).toFixed(1));
        component.percentPlayed = position;
      });
    },
    onSetIframeRef(iframeRef) {
      this.iframeRef = iframeRef;
      loadScript(soundcloudApi, () => {
        this.soundcloud = SC.Widget(this.iframeRef);
        this.bindSoundcloudEvents();
      });
    },
    setCurrentTrack(track, index) {
      this.currentTrack = {
        artist: track.user.username,
        artist_url: track.user.permalink_url,
        background: track.artwork_url || (track.user && track.user.avatar_url) || '',
        duration: track.duration,
        permalink_url: track.permalink_url,
        title: track.title
      }
      this.trackIndex = index;
    }
  }
}
</script>
