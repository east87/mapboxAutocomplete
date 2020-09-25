<template>
  <div>
    <p></p>

    <MapboxGeocoder
      :access-token="accesstoken"
      :types="types"
      :limit="limit"
      :zoom="18"
      externalGeocoder="GeoJSON"
      :reverseGeocode="reverseGeocode"
      placeholder="search address"
      @mb-result="onComplete"
    />
    <p>
      locations
      {{ form.country + "-" + form.region + "-" + form.lat + "-" + form.lng }}
    </p>
  </div>
</template>

<script>
import _ from "lodash";
import { MapboxGeocoder } from "@studiometa/vue-mapbox-gl";
import "@mapbox/mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css";
export default {
  name: "geocoder",
  components: {
    //  mapboxgl,
    MapboxGeocoder,
  },
  props: {
    country: { type: [Array, Object], default: () => [] },
    region: { type: [Array, Object], default: () => [] },
    place: { type: [Array, Object], default: () => [] },
    locality: { type: [Array, Object], default: () => [] },
  },
  data() {
    return {
      types:
        "poi,address,neighborhood,locality,place,district,postcode,region,country",
      accesstoken:
        "pk.eyJ1IjoiZWFzdDg3IiwiYSI6ImNrZmk0Y3BsOTAzY2kzMHFqNHg3eW13MTAifQ.WQGNi1Pk1HHtZrzreVYy7w",
      onblur: true,
      reverseGeocode: true,
      limit: 15,
      form: {
        country: "dadas",
        region: null,
        place: null,
        locality: null,
        lat: null,
        lng: null,
      },
    };
  },
  methods: {
    onComplete(result) {
      // var respons = JSON.stringify(result);
      const responsmap = Object.keys(result).map((key) => result[key]);
      //console.log(result);

      var country = [];
      var region = [];
      var place = [];
      var locality = [];
      var country_name = null;
      var country_id = null;
      var region_id = null;
      var region_name = null;
      var place_id = null;
      var place_name = null;
      var locality_id = null;
      var locality_name = null;
      var lat = responsmap[0].center[1];
      var lng = responsmap[0].center[0];

      if (!responsmap[0].context) {
        country_id = responsmap[0].id;
        country_name = responsmap[0].text;
        region_id = "";
        region_name = "";
        place_id = "";
        place_name = "";
        locality_id = "";
        locality_name = "";
        //  console.log(responsmap[0].id);
      } else {
        var collection = responsmap[0].context;
        country = _.filter(collection, function (item) {
          return item.id.indexOf("country.") > -1;
        });
        country_id = country[0].id;
        country_name = country[0].text;

        region = _.filter(collection, function (item) {
          return item.id.indexOf("region.") > -1;
        });
      
        region_id = region[0].id;
        region_name = region[0].text;

        place = _.filter(collection, function (item) {
          return item.id.indexOf("place.") > -1;
        });
        place_id = place[0].id;
        place_name = place[0].text;

        locality = _.filter(collection, function (item) {
          return item.id.indexOf("locality.") > -1;
        });
        locality_id = locality[0].id;
        locality_name = locality[0].text;
      }

      //console.log(responsmap[0])
      // console.log(lat)
      // console.log(lng)
      this.form.country = country_name;
      this.form.region = region_name;
      this.form.place = place_name;
      this.form.locality = locality_name;
      this.form.lng = lng;
      this.form.lat = lat;
    },
  },
};
</script>
