<script setup>
// // Google Maps API setup
(g => {

// variables
var h, a, k,
    p = "The Google Maps JavaScript API",
    c = "google",
    l = "importLibrary",
    q = "__ib__",
    m = document,
    b = window;

// check for a google object
b = b[c] || (b[c] = {});

// check for a maps object in the google object
var d = b.maps || (b.maps = {}),
    r = new Set(),
    e = new URLSearchParams(),
    
    // load google maps script if it hasn't loaded
    u = () => h || (h = new Promise(async (f, n) => {
      
      // create script element and setup libraries and paramenters
      await (a = m.createElement("script"));      
      e.set("libraries", [...r] + "");      
      for (k in g) {
        e.set(k.replace(/[A-Z]/g, t => "_" + t[0].toLowerCase()), g[k]);
      }      
      e.set("callback", c + ".maps." + q);      
      a.src = `https://maps.${c}apis.com/maps/api/js?` + e;      
      d[q] = f;
      
      // set error handler
      a.onerror = () => h = n(Error(p + " could not load."));      
      a.nonce = m.querySelector("script[nonce]")?.nonce || "";
      
      // Append the script element to the doc head
      m.head.append(a);
    }));

// load the import library if it hasn't loaded, log a warning if it has.
d[l] ? console.warn(p + " only loads once. Ignoring:", g) 
     : d[l] = (f, ...n) => r.add(f) && u().then(() => d[l](f, ...n));

})({
key: "AIzaSyCRNLdJoO4TDB5lGjO7Ot0lx2KhgjF36zw", 
v: "beta"
});


 let map;








async function initMap() {
  // The location of Office
  const position_1 = { lat: -37.847350, lng: 145.114552 };
  const position_2 = { lat: -37.820576, lng: 144.950294 };
  // Request needed libraries.
  const { Map } = await google.maps.importLibrary("maps");
  const { AdvancedMarkerElement } = await google.maps.importLibrary("marker");

  // The map, centered at Office
  map = new Map(document.getElementById("map"), {
    zoom: 11,
    center: position_1,
    mapId: "DEMO_MAP_ID",
  });

  // The marker, positioned at Office
  const marker = new AdvancedMarkerElement({
    map: map,
    position: position_1,
    title: "Office",
  });

  // The marker, positioned at Office
  const marker_2 = new AdvancedMarkerElement({
  map: map,
  position: position_2,
  title: "Office-2",
});

  // Create an InfoWindow
  const infoWindow = new google.maps.InfoWindow({
      content: "Corporate Office",
  });

  // Create an InfoWindow
  const infoWindow_2 = new google.maps.InfoWindow({
      content: "City Office",
  });

  // Adding click event listener to the marker to open the InfoWindow
  marker.addEventListener('gmp-click', () => {
    infoWindow.open({
      anchor: marker,
      map,
      shouldFocus: false,
    });
  });

  // Adding click event listener to the marker to open the InfoWindow
  marker_2.addEventListener('gmp-click', () => {
    infoWindow_2.open({
      anchor: marker_2,
      map,
      shouldFocus: false,
    });
  });
}

initMap();

</script>



<template>
  <div class="about">
    <h1>About us</h1>
    <div id="map"></div>
    <iframe src="https://www.google.com/maps/embed?pb=!1m17!1m12!1m3!1d116473.26298195997!2d144.97113484740262!3d-37.85160191083259!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m2!1m1!2zMzfCsDUwJzUwLjUiUyAxNDXCsDA2JzUyLjQiRQ!5e0!3m2!1sen!2sau!4v1694939882686!5m2!1sen!2sau" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>

  </div>
</template>

<style>
#map {
  height: 400px;
  width: 100%;
}
</style>
