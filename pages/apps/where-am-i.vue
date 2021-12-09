<template>
  <div class="container">
    <div id="map"></div>
  </div>
</template>

<script>
import { Map, View } from "ol";
import TileLayer from "ol/layer/Tile";
import XYZ from "ol/source/XYZ";
import { fromLonLat } from "ol/proj";

export default {
  name: "WhereAmI",
  data() {
    return {
      view: null,
    };
  },
  created() {
    this.$store.commit("setTitle", this.$metaInfo.title);
  },
  mounted() {
    this.initializeMap();
    this.getUserPosition();
  },
  methods: {
    initializeMap() {
      this.view = new View({
        center: [0, 0],
        zoom: 2,
      });

      new Map({
        target: "map",
        layers: [
          new TileLayer({
            source: new XYZ({
              url: "https://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png",
            }),
          }),
        ],
        view: this.view,
      });
    },
    getUserPosition() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((pos) => {
          const userPosition = [pos.coords.longitude, pos.coords.latitude];
          const globalPosition = fromLonLat(userPosition);

          console.log(userPosition, globalPosition);

          this.view.setCenter(globalPosition);

          const interval = setInterval(() => {
            if (this.view.getZoom() > 17) clearInterval(interval);

            this.view.setZoom(this.view.getZoom() + 1);
          }, 1500);
        });
      }
    },
  },
  head() {
    return {
      title: "Where Am I",
    };
  },
};
</script>

<style scoped>
.container {
  position: relative;
  height: 100%;
}

#map {
  position: absolute;
  inset: 0;
}
</style>
