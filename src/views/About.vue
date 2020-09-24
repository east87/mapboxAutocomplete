<template>
  <mapbox-map
    style="height: 400px"
    :access-token="accesstoken"
    map-style="mapbox://styles/mapbox/streets-v11"
    :center="[0, 0]"
    :zoom="1">
    <mapbox-marker :lng-lat="[0, 0]" popup>
      <template v-slot:popup>
        <p>Hello world!</p>
      </template>
    </mapbox-marker>
  </mapbox-map>
</template>

<script>
//import mapboxgl from 'mapbox-gl';
import { MapboxMap, MapboxMarker } from '@studiometa/vue-mapbox-gl';
import 'mapbox-gl/dist/mapbox-gl.css';
export default {
  name: "geocoder",
  components: {
  //  mapboxgl,
 MapboxMap,
 MapboxMarker
  },

  data() {
    return {
      accesstoken: "pk.eyJ1IjoiZWFzdDg3IiwiYSI6ImNrZjUzNHFlcjA0d2cyeWp4OWliYTkwdDcifQ.oovHlSDtUv7JTimvnpRl2Q",
      
    };
  },
  methods: {
    onComplete() {
      alert("Submitting Form ! Rock On");
    },
  },
};
</script>