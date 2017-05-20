# vue-twitch-player [![license](https://img.shields.io/github/license/tserkov/vue-twitch-player.svg)]()
A Vue component for embedding a Twitch player. See component for all available properties.

[Vue-plugin-load-script](https://github.com/tserkov/vue-plugin-load-script) is a dependency, since the Twitch Player API needs to be included from Twitch's servers.

## Install

``` bash
# npm
npm install --save-dev vue-twitch-player
```

``` bash
# yarn
yarn add --dev vue-twitch-player
```

## Use

```javascript
  // In main.js
  import LoadScript from 'vue-plugin-load-script';

  Vue.use(LoadScript);
```

```html
<template>
  <twitch-player
    :channel="channel"
  ></twitch-player>
</template>

<script>
  import VueTwitchPlayer from 'vue-twitch-player';

  export default {
    // ...
    components: {
      VueTwitchPlayer,
    },
    data() {
      return {
        channel: 'tserkov',
      };
    },
    // ...
  };
</script>
```

```html
<template>
  <twitch-player
    :video="video"
  ></twitch-player>
</template>

<script>
  import VueTwitchPlayer from 'vue-twitch-player';

  export default {
    // ...
    components: {
      VueTwitchPlayer,
    },
    data() {
      return {
        video: '117216248',
      };
    },
    // ...
  };
</script>
```

```html
<template>
  <twitch-player
    :collection="collection"
  ></twitch-player>
</template>

<script>
  import VueTwitchPlayer from 'vue-twitch-player';

  export default {
    // ...
    components: {
      VueTwitchPlayer,
    },
    data() {
      return {
        collection: 'TbyX29kRqhRnxA',
      };
    },
    // ...
  };
</script>
```
