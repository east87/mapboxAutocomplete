<template>
  <mapbox-geocoder :access-token="accesstoken" @mb-results="onComplete" />
</template>

<script>
//import mapboxgl from 'mapbox-gl';
import { MapboxGeocoder } from '@studiometa/vue-mapbox-gl';
import "@mapbox/mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css";
export default {
  name: "geocoder",
  components: {
  //  mapboxgl,
 MapboxGeocoder
  },

  data() {
    return {
      accesstoken: "pk.eyJ1IjoiZWFzdDg3IiwiYSI6ImNrZjUzNHFlcjA0d2cyeWp4OWliYTkwdDcifQ.oovHlSDtUv7JTimvnpRl2Q",
      
    };
  },
  methods: {
    onComplete(results) {
      console.log(results);
    },
  },
};
</script>