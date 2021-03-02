<template>
  <div id="map" class="map" ref="map"></div>
</template>

<script>
export default {
  head(){
    return {
      title: 'treasures!',
      script: [{
        src:'https://maps.googleapis.com/maps/api/js?key=AIzaSyByIgrPcKwA5P3UintyMzkV1LRVsM303ss&callback=initMap',
        defer: true,
        hid: 'map'
      }]
    };
  },
  mounted(){
    // @ts-ignore
    window.initMap = this.initMap;
  },
  data() {
    return {
      map: null
    }
  },
  methods: {
    initMap() {
      if (navigator.geolocation) {
        navigator.geolocation.watchPosition((position) => {
          if (this.map) this.map.setCenter(new window.google.maps.LatLng(position.coords.latitude, position.coords.longitude));
          else this.setupMap(position.coords);
        })
      }
    },
    setupMap(center) {
      const mapOptions = {
        zoom: 18,
        center: new window.google.maps.LatLng(center.latitude, center.longitude),
        disableDefaultUI: true,
        zoomControl: false,
        scrollwheel: false,
        gestureHandling: "none"
      };

      this.map = new window.google.maps.Map(this.$refs.map,mapOptions)
    }
  }
}
</script>

<style lang="scss">
.map {
  width: 100%;
  height: 400px;
}
</style>
