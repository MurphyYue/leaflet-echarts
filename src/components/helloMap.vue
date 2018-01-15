<template>
<div id="map"></div>  
</template>
<script>
import leaflet from "leaflet";
import mapProvider from "../common/js/mapProviders.js";
import * as echarts from 'echarts';
import icon from "leaflet/dist/images/marker-icon.png";
import iconShadow from "leaflet/dist/images/marker-shadow.png";

/* const MAP_IMAGE_PATH = "../common/images/leaflet/"; */
export default {
  data() {
    return {
      map: null,
      markers: null,
      circle: null,
      polygon: null,
      mapChart: null,
      geoJsonLayer: null,
      init_map_data: null,
      reset_btn: null,
      map_config: {
        zoom: 15,
        center: [39.92, 116.392],
        minZoom: 3,
        maxZoom: 18,
        attribution: "&copy; 高德地图"
      },
      option: {
            title: {
                text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
                data:['销量']
            },
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        }
    };
  },
  mounted() {
    this.initMap();
    this.addSymble()
  },
  methods: {
    /* initMap() {
      L.Icon.Default.imagePath = MAP_IMAGE_PATH;

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
      /*  L.Icon.Default.imagePath = MAP_IMAGE_PATH; */
      let DefaultIcon = L.icon({
        iconUrl: icon,
        shadowUrl: iconShadow
      });
      L.Marker.prototype.options.icon = DefaultIcon;
      this.map = L.map("map", {
        center: this.map_config.center,
        zoom: this.map_config.zoom,
        minZoom: this.map_config.minZoom,
        maxZoom: this.map_config.maxZoom,
        zoomControl: false
        // scrollWheelZoom: false,
      });
      L.tileLayer
        .mapProvider("GaoDe.Normal.Map", {
          attribution: this.map_config.attribution
        })
        .addTo(this.map);
      
      L.control.zoom({
        zoomInTitle: '放大',
        zoomOutTitle: '缩小'
      }).addTo(this.map)
    },
    addSymble() {
      this.markers = L.marker(this.map_config.center).addTo(this.map);
      this.circle = L.circle([39.92, 116.392],{
        color: 'red',
        fillColor: '#f03',
        fillOpacity: 0.5,
        radius: 500
      }).addTo(this.map)
      this.polygon = L.polygon([
        [39.91, 116.392],
        [39.92, 116.397],
        [39.92, 116.392]
      ]).addTo(this.map)
      this.markers.bindPopup("<div id='mapChart'></div>")
      this.markers.on('click',this.drawChart)
    },
    drawChart() {
      this.mapChart = echarts.init(document.getElementById('mapChart'))
      this.mapChart.setOption(this.option)
    }

  }
};
</script>
<style>
@import "../../node_modules/leaflet/dist/leaflet.css";

#map {
  height: 100vh;
}
#mapChart{
  width: 200px;
  height: 150px;
}
</style>



