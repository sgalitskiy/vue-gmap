<template>
  <div>
    <div class="google-map" ref="googleMap" :style="style"></div>
    <template v-if="!!this.map">
      <slot
        :map="map"
      />
    </template>

  </div>
</template>

<script>
const defaultHeight = 400; // px

export default {
  props: {
    google: {
      type: Object,
      required: true,
    },
    mapConfig: Object,
    height: Number,
    width: Number,
  },

  data() {
    return {
      map: null,
    };
  },

  mounted() {
    this.initializeMap();
  },

  computed: {
    style() {
      let style = {
        height: (this.height || defaultHeight) + 'px',
      };

      if (this.width) {
        style = {
          ...style,
          width: this.width + 'px',
        };
      }

      return style;
    },
  },

  methods: {
    initializeMap() {
      const mapContainer = this.$refs.googleMap;
      this.map = new this.google.maps.Map(mapContainer, this.mapConfig);
    },
  },
};
</script>
