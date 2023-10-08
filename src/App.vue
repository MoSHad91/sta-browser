<template>

<div class="grid grid-cols-6 gap-1">
    <div class="main-left col-span-1 space-y-0">
      <div class="sidenav">
        <a href="#title">STA Browser</a>

      </div>           
    </div>
    <div class="main-right col-span-5  space-y-0">
      <div id="mapContainer"></div>

    </div>

</div>



</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";


export default {
  name: "LeafletMap",
  data() {
    return {
      map: null,
    };
  },
  mounted() {
    this.map = L.map("mapContainer").setView([46.05, 11.05], 5);
    L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
    }).addTo(this.map);
    //use a mix of renderers
    var customPane = this.map.createPane("customPane");
    var canvasRenderer = L.canvas({ pane: "customPane" });
    customPane.style.zIndex = 399; // put just behind the standard overlay pane which is at 400
    L.marker([50, 14]).addTo(this.map);

    L.marker([53, 20]).addTo(this.map);
    L.marker([49.5, 19.5]).addTo(this.map);
    L.marker([49, 25]).addTo(this.map);
    L.marker([-10, 25]).addTo(this.map);
    L.marker([10, -25]).addTo(this.map);
    L.marker([0, 0]).addTo(this.map);

  },
  onBeforeUnmount() {
    if (this.map) {
      this.map.remove();
    }
  },
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
}
html, body {
  margin: 0;
  padding: 0;
}

main {
  height: 100%;
  width: 100%;
}
.sidenav {
  height: 100vh;
  width: 100%;
  position: relative;
  z-index: 1;
  top: 0;
  left: 0;
  background-color: #111;
  overflow-x: hidden;
  padding-top: 20px;
}

.sidenav a {
  padding: 6px 8px 6px 16px;
  text-decoration: none;
  font-size: 25px;
  color: #818181;
  display: block;
}

.sidenav a:hover {
  color: #f1f1f1;
}


#mapContainer {
  width: 100%;
  height: 100vh;
}
@media screen and (max-height: 450px) {
  .sidenav {padding-top: 15px;}
  .sidenav a {font-size: 18px;}
}

</style>
