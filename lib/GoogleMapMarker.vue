<template>
  <div class="wrapper">
    <div :id="id">
      <h1>Item details</h1>
      <p>{{JSON.stringify(marker.position)}}</p>
    </div>
  </div>
</template>

<style lang="scss">
  .wrapper {display: none}
</style>

<script>
import Icon from './icon.svg';

export default {
  props: {
    google: {
      type: Object,
      required: true,
    },
    map: {
      type: Object,
      required: true,
    },
    marker: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      point: null,
      infoWindow: null,
    };
  },

  mounted() {
    this.point = new this.google.maps.Marker({
      position: this.marker.position,
      map: this.map,
      title: JSON.stringify(this.marker.position),
      icon: Icon,
    });

    this.point.addListener('click', () => this.showPopup(this.map, this.point));
  },

  computed: {
    id() {
      return `info_${this.marker.id}`;
    },
  },

  methods: {
    showPopup(map, point) {
      if (!this.infoWindow) {
        this.infoWindow = new this.google.maps.InfoWindow({
          content: document.getElementById(this.id),
        });
      }

      this.infoWindow.open(map, point);
    },
  },
};
</script>
