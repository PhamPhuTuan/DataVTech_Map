<template>
  <div class="map-wrap">
    <div class="map" ref="mapContainer"></div>
  </div>
</template>
  
<script>
import { Map, NavigationControl, Marker, Popup } from 'maplibre-gl';
import { shallowRef, onMounted, onUnmounted, markRaw } from 'vue';

export default {
  name: "MapItem",
  setup() {

    const mapContainer = shallowRef(null);
    const map = shallowRef(null);

    onMounted(() => {
      const apiKey = 'ncRcqEU0Bhtvd3HPqyCG';
      const initialState = { lng: 144.964635, lat: -37.816938, zoom: 14 };

      map.value = markRaw(new Map({
        container: mapContainer.value,
        style: `https://api.maptiler.com/maps/streets-v2/style.json?key=${apiKey}`,
        // center: [initialState.lng, initialState.lat],
        zoom: initialState.zoom
      }));

      map.value.addControl(new NavigationControl(), 'top-right');
      
      let listJob = location.href.split('start:')[1].split('~') || [1, 2, 3];
      
      for( let i = 0; i < listJob.length; i+=3) {
        map.value.setCenter([130.964635 + Number.parseFloat(listJob[1]), -52.816938 + Number.parseFloat(listJob[2])])
        const popup = new Popup({ offset: 25 }).setText(
          `Job: ${listJob[i+0]}`
        );
        new Marker({ color: "#FF0000", ariaLabel: listJob[0] })
          .setLngLat([130.964635 + Number.parseFloat(listJob[i+1]), -52.816938 + Number.parseFloat(listJob[i+2])])
          .setDraggable(false)
          .setPopup(popup)
          .addTo(map.value);
      }

      
      // new Marker({ color: "#FF0000", accessKeyLabel: "asfhkas" })
      //   .setLngLat([144.960814, -37.816874])
      //   .setDraggable(true)
      //   .addTo(map.value);
      // new Marker({ color: "#FF0000", localName: "asdfafa" })
      //   .setLngLat([144.969441, -37.814156])
      //   .setDraggable(true)
      //   .addTo(map.value);
      // new Marker({ color: "#FF0000" })
      //   .setLngLat([144.960455, -37.813426])
      //   .setDraggable(true)
      //   .addTo(map.value);
      // const popup = new Popup({ offset: 25 }).setText(
      //   'Job: SRV00000Biet'
      // );
      // new Marker({ color: "#000000" })
      //   .setLngLat([144.992883, -37.847992])
      //   .setPopup(popup)
      //   .addTo(map.value);
    }),
      onUnmounted(() => {
        map.value?.remove();
      })

    return {
      map, mapContainer
    };
  }
};
</script>
  
  
<style scoped>
@import '~maplibre-gl/dist/maplibre-gl.css';

.map-wrap {
  position: relative;
  width: 100vw;
  height: 100vh;
}

.map {
  position: absolute;
  width: 100%;
  height: 100%;
}

.watermark {
  position: absolute;
  left: 10px;
  bottom: 10px;
  z-index: 999;
}
</style>