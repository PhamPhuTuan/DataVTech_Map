<template>
  <div>
    <div id="header">
      <div id="logo">
        <img id="imgHeader" height="40" width="40" src="../public/187176214_1764406580595110_5693802133054958028_n.jpeg"/>
        Data V Tech
      </div>
      <h5 style="color: black">Coordinates: {{ lng }} , {{ lat }}</h5>
    </div>
    <GoogleMap
      api-key="AIzaSyCTrGWB4AcVPfw8GDmVG5JTY2vrlZ2akc4"
      style="width: 100vw; height: 100vh; bottom: 0;"
      :center="center"
      :zoom="15"
      @click="MapClick"
    >
      <Marker
        v-for="(item, idx) in geojson.features"
        :key="idx"
        :options="{ position: item.geometry.coordinates }"
      >
        <InfoWindow
          v-if="item.geometry.name"
          :options="{
            position: item.geometry.coordinates,
            content: item.geometry.name
          }"
        />
      </Marker>
    </GoogleMap>
  </div>
</template>

<script>
import { GoogleMap, Marker, InfoWindow } from "vue3-google-map";
export default {
  name: "App",
  components: {
    GoogleMap,
    Marker,
    InfoWindow,
  },
  data() {
    return {
      lng: 0,
      lat: 0,
      center: { lat: -34.94536477255069, lng: 138.55101730228625 },
      geojson: {
        type: "FeatureCollection",
        features: [
          {
            type: "Feature",
            geometry: {
              type: "Point",
              name: "Andrew",
              display: "true",
              coordinates: { lat: -34.94536477255069, lng: 138.55101730228625 },
            },
            properties: {
              title: "Mapbox",
              description: "Washington, D.C.",
            },
          },
          {
            type: "Feature",
            geometry: {
              type: "Point",
              name: "Phu Tuan",
              coordinates: {lat: -34.933825692138065, lng: 138.55146791340076},
            },
            properties: {
              title: "Mapbox",
              description: "Washington, D.C.",
            },
          },
          {
            type: "Feature",
            geometry: {
              type: "Point",
              name: "Andrew",
              coordinates: { lat: -34.94536477255069, lng: 138.55101730228625 },
            },
            properties: {
              title: "Mapbox",
              description: "Washington, D.C.",
            },
          },
        ],
      },
    };
  },

  methods: {
    MapClick(event) {
      this.geojson.features.pop();
      let coor = { lat: 0, lng: 0 };
      coor = event.latLng.toJSON();
      this.lat = coor.lat;
      this.lng = coor.lng;
      this.geojson.features.push({
        type: "Feature",
        geometry: {
          type: "Point",
          coordinates: coor,
        },
        properties: {
          title: "Mapbox",
          description: "San Francisco, California",
        },
      });
    },
  },
};
</script>

<style lang="scss">
@import "~vue-maplibre-gl/src/css/maplibre.scss";

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
    "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
    monospace;
}

#app {
  width: 100%;
  height: 100vh;
}

#header {
  height: 40px;
  width: 70vw;
  align-content: center;
  align-items: center;
  line-height: 40px;
  background-color: white;
  position: fixed;
  top:0;
  margin-left: 15vw;
  text-align: center;
  font-size: 30px;
  color: #7ec442;
  z-index: 10;
  display: flex;
  justify-content: space-around;
}
#logo {
  align-content: center;
  align-items: center;
  display: flex;
  line-height: 40px;
  text-align: center;
}
#imgHeader {
  margin-right: 20px;
}

#mapapp {
  height: 80vh;
}

.gmnoprint {
  z-index: 11;
}

.mapboxgl-popup {
  max-width: 200px;
}

.mapboxgl-popup-content {
  text-align: center;
  font-family: "Open Sans", sans-serif;
}
</style>
