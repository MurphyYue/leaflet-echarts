<template>
<div id="map"></div>  
</template>
<script>
import leaflet from "leaflet";
import mapProvider from "../common/js/mapProviders.js";

//const MAP_IMAGE_PATH = "../../node_modules/leaflet/dist/images/";
export default {
  data() {
    return {
                map: null,
                markers: null,
                geoJsonLayer: null,
                init_map_data: null,
                reset_btn: null,
                map_config: {
                    zoom: 15,
                    center: [39.92, 116.39],
                    minZoom: 3,
                    maxZoom: 18,
                    attribution: "&copy; 高德地图",
                },
            };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    /* initMap() {
      //L.Icon.Default.imagePath = MAP_IMAGE_PATH;

      this.mymap = L.map("map").setView([39.9, 116.36], 13)
      L.tileLayer(
        "https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}",
        {
          attribution:
            'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://mapbox.com">Mapbox</a>',
          maxZoom: 18,
          id: "mapbox.streets",
          accessToken: "pk.eyJ1IjoibXVycGh5eXVlIiwiYSI6ImNqY2Jtajg3bDBzN3cyeXA1dTkzcGtlMm4ifQ.jXvKC9c52eEXYryHQVp1yQ"
        }
      ).addTo(this.mymap);
    } */
    initMap() {
      this.map = L.map("map", {
        center: this.map_config.center,
        zoom: this.map_config.zoom,
        minZoom: this.map_config.minZoom,
        maxZoom: this.map_config.maxZoom
        // scrollWheelZoom: false,
      });
      L.tileLayer
        .mapProvider("GaoDe.Normal.Map", {
          attribution: this.map_config.attribution
        })
        .addTo(this.map);
    }
  }
};
</script>
<style>
@import "../../node_modules/leaflet/dist/leaflet.css";

#map {
  height: 100vh;
}
</style>



