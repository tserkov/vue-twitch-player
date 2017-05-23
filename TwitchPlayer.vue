<template>
  <div :id="playerId"></div>
</template>

<script>
  import Vue from 'vue';
  import LoadScript from 'vue-plugin-load-script';

  Vue.use(LoadScript);

  let player;

  export default {
    name: 'twitch-player',
    props: {
      width: {
        type: String,
        default: '400',
      },
      height: {
        type: String,
        default: '300',
      },
      initialVolume: {
        type: Number,
        default: 0.5,
      },
      initialQuality: {
        type: String,
        default: 'medium',
      },
      channel: String,
      collection: String,
      video: String,
    },
    data() {
      return {
        playerId: `twitch-player-${this._uid}`, // eslint-disable-line no-underscore-dangle
      };
    },
    beforeCreate() {
      Vue.loadScript('//player.twitch.tv/js/embed/v1.js')
        .then(() => {
          const options = {
            width: this.width,
            height: this.height,
          };

          if (this.channel) {
            options.channel = this.channel;
          } else if (this.collection) {
            options.collection = this.collection;
          } else if (this.video) {
            options.video = this.video;
          } else {
            // Error: No specified source!
          }

          player = new window.Twitch.Player(this.playerId, options); // eslint-disable-line no-underscore-dangle, max-len

          player.addEventListener('ended', () => (this.$emit('ended')));

          player.addEventListener('pause', () => (this.$emit('pause')));

          player.addEventListener('play', () => (this.$emit('play')));

          player.addEventListener('offline', () => (this.$emit('offline')));

          player.addEventListener('online', () => (this.$emit('online')));

          player.addEventListener('ready', () => {
            player.setQuality(this.initialQuality);
            player.setVolume(this.initialVolume);
          });
        }).catch((e) => (this.$emit('error', e)));
    },
    methods: {
      play() {
        player.play();
      },
      pause() {
        player.pause();
      },
      seek(timestamp) {
        player.seek(timestamp);
      },
      getVolume() {
        return player.getVolume();
      },
      isMuted() {
        return player.getMuted();
      },
      mute() {
        player.setMuted(true);
      },
      unmute() {
        player.setMuted(false);
      },
    },
    watch: {
      channel(newChannel) {
        player.setChannel(newChannel);
      },
      collection(newCollection) {
        player.setCollection(newCollection);
      },
      video(newVideo) {
        player.setVideo(newVideo);
      },
      volume(newVolume) {
        player.setVolume(newVolume);
      },
      quality(newQuality) {
        if (player.getQualities().indexOf(newQuality) !== -1) {
          player.setQuality(newQuality);
        }
      },
    },
  };
</script>
