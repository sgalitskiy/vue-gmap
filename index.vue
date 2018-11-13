<template>
  <div>
    <h1>Map 1. {{datetime}}</h1>
    <GoogleMapLoader
      :apiKey="apiKey"
    >

      <template slot-scope="{ google }">
        <GMap
          :mapConfig="mapConfig"
          :google="google">

          <template slot-scope="{ map }">
            <GoogleMapMarker
              v-for="marker in markers"
              :key="marker.id"
              :marker="marker"
              :google="google"
              :map="map"
            />

            <GoogleMapLines
              v-for="line in lines"
              :key="line.id"
              :path="line.path"
              :google="google"
              :map="map"
            />

          </template>
        </GMap>

        <div>
          <h2>Map 2</h2>
          <GMap :mapConfig="mapConfig"
                :height="100"
                :google="google"/>
        </div>

        <div>
          <h2>Map 3</h2>
          <GMap :mapConfig="mapConfig"
                :height="200"
                :width="200"
                :google="google"/>
        </div>


      </template>


    </GoogleMapLoader>
  </div>
</template>

<script>
import GoogleMapLoader from './lib/GoogleMapLoader.vue';
import GMap from './lib/GMap.vue';
import GoogleMapMarker from './lib/GoogleMapMarker.vue';
import GoogleMapLines from './lib/GoogleMapLines.vue';

const mapSettings = {
  clickableIcons: false,
  streetViewControl: false,
  panControlOptions: false,
  gestureHandling: 'cooperative',
  mapTypeControl: false,
  zoom: 5,
  zoomControlOptions: {
    style: 'SMALL',
  },
  minZoom: 2,
  maxZoom: 16,
};

export default {
  components: {
    GoogleMapLoader,
    GMap,
    GoogleMapMarker,
    GoogleMapLines,
  },
  data() {
    return {
      list: [
        {
          lat: 41.3851, lng: 2.1734,
        },
        {
          lat: 48.8566, lng: 2.3522,
        },
        {
          lat: 51.5074, lng: 0.1278,
        },
      ],

      datetime: new Date().toLocaleString(),
      apiKey: 'your_API_key_here',
    };
  },
  computed: {
    markers() {
      return this.list.map(item => ({
        id: item.lat + '' + item.lng,
        position: item,
      }));
    },

    lines() {
      let lines = [];
      for (let i = 0; i < this.list.length - 1; i + 1) {
        lines.push({
          id: this.list[i].lat + '_' + this.list[i].lng,
          path: [this.list[i], this.list[i + 1]],
        });
      }

      return lines;
    },

    mapConfig() {
      return {
        ...mapSettings,
        center: this.markers[0].position,
      };
    },
  },
};
</script>
