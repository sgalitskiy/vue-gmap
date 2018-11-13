<script>
const config = {
  clickable: false,
  geodesic: false,
  strokeOpacity: 0,
  strokeColor: '#00FF00',
  icons: [
    {
      icon: {
        path: 'M 0,-2 0,2',
        strokeOpacity: 1,
        strokeWeight: 2,
        scale: 1,
      },
      repeat: '10px',
    },
  ],
};

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
    path: {
      type: Array,
      required: true,
    },
  },

  data() {
    return {
      line: null,
    };
  },

  mounted() {
    this.line = new this.google.maps.Polyline({
      path: this.path,
      map: this.map,
      ...config,
    });
  },
};
</script>
