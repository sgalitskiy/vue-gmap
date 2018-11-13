<template>
  <div>
    <template v-if="Boolean(this.google)">
      <slot
        :google="google"
      />
    </template>
  </div>
</template>

<style lang="scss">

</style>

<script>

import GoogleMapsApiLoader from 'google-maps-api-loader';

export default {
  name: 'GoogleMapLoader',
  props: {
    apiKey: String,
  },

  data() {
    return {
      google: null,
    };
  },

  async mounted() {
    const googleMapApi = await GoogleMapsApiLoader({
      apiKey: this.apiKey,
    });
    this.google = googleMapApi;
  },
};
</script>
