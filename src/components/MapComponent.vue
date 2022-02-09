<template>
  <div id="map"></div>
</template>

<script>
import mapboxgl from "mapbox-gl";

export default {
  name: "MapComponent",
  data: () => ({
    map: {
      type: Object,
      default: null,
    },
  }),
  mounted() {
    if (navigator.onLine && mapboxgl.supported()) {
      const post = fetch("https://am.i.mullvad.net/json").then((r) => r.json());
      console.log(post);
      mapboxgl.accessToken =
        "pk.eyJ1IjoibGFua2xpc3EiLCJhIjoiY2t6Y2p4dGp4MDExNDMycGRydzM3N2ozZiJ9.MUkQ9fVe1-f0FSday6Fgag";
      this.map = new mapboxgl.Map({
        container: "map", // container ID
        style: "mapbox://styles/mapbox/streets-v11", // style URL
        center: [-74.5, 40], // starting position [lng, lat]
        zoom: 9, // starting zoom
        cooperativeGestures: true,
        projection: "naturalEarth",
      });
      this.map.addControl(new mapboxgl.FullscreenControl());
      this.map.addControl(new mapboxgl.NavigationControl());
    } else {
      window.alert("You are offline!");
    }
  },
  methods: {
    getLocation() {},
  },
};
</script>

<style scoped>
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
</style>
