<html lang="en">
<head>
  <meta charset="utf-8">

  <title>Simple Map</title>
  <meta name="description" content="Testing out basic Leaflet">

  <!-- YOUR STYLES HERE -->
  <!-- Step 1. Paste Leaflet CSS here -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
  integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
  crossorigin=""/>

  <!-- Step 2. Paste Leaflet JS here -->
  <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
   integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
   crossorigin=""></script>

   <style>
    .container {
        margin-left: 15px;
        margin-right: 15px;
        text-align: center;
    }

    .centerobject {
        display: block;
        margin-left: auto;
        margin-right: auto;
    }

    /* Step 4. Define the map window by ID. */

    #mapid { 
        height: 400px;
        width: 400px;
    }
   </style>
</head>

<body>
    <div class="container">
        <h1>Map Sample - London</h1>
    </div>

    <!-- Step 3. Create the div to contain the map. -->
    <div id="mapid" class="centerobject">
    </div>

  <!-- YOUR JAVASCRIPT HERE -->
  <script>
    // Step 5. Create a map in the <div> with class map ID
    // with the specified coordinates (in array), and zoom level.
    // This creates an empty View wondow.
    let mymap = L.map('mapid').setView([51.505, -0.09], 10);

    // Step 7. Adding a marker
    let marker = L.marker([51.5, -0.09]).addTo(mymap);

    // Step 8. Adding a circle
    let circle = L.circle([51.508, -0.11], {
        color: 'green',
        fillColor: '#a0f765',
        fillOpacity: 0.5,
        radius: 500
    }).addTo(mymap);

    // Step 9. Adding a polygon
    let polygon = L.polygon([
        [51.509, -0.08],
        [51.501, -0.13],
        [51.503, -0.06],
        [51.51, -0.047]
    ]).addTo(mymap);

    // Step 10. Adding pop-ups to markers, circles and polygons.
    // Only the markers make use of the openPopup function.
    marker.bindPopup("<b>Hello world!</b><br>I am a popup.").openPopup();
    circle.bindPopup("I am a circle.");
    polygon.bindPopup("I am a polygon.");

    // Step 11. Setting standalone popups.
    let popup = L.popup()
    .setLatLng([51.5, -0.09])
    .setContent("I am a standalone popup.")
    .openOn(mymap);

    // Step 12. Interacting with the map
    /*function onMapClick(e) {
    alert("You clicked the map at " + e.latlng);
    }*/

    //mymap.on('click', onMapClick);

    // Step 13. Replacing alerts in the above example with popups:
    let coordPopup = L.popup();

    function onMapClick(e) {
    coordPopup
        .setLatLng(e.latlng)
        .setContent("You clicked the map at " + e.latlng.toString())
        .openOn(mymap);
    }

    mymap.on('click', onMapClick);



    // Step 6. Adding the tiles. I use ThunderForest.
    // Note that you also need an access token.
    L.tileLayer('https://tile.thunderforest.com/neighbourhood/{z}/{x}/{y}.png?apikey=e6af7839f94a43428e202e1290e0a2be', {
        // Change attribution to reflect your map provider
        attribution: 'Map data &copy; <a href="https://manage.thunderforest.com">Thunderforest</a> contributors, Imagery © <a href="https://manage.thunderforest.com/">Thunderforest</a>',
        maxZoom: 18,
        // ID is Mapbox specific, and isn't required for Thunderforest.
        //id: 'thunderforest/streets-v11',
        tileSize: 512,
        // zoomOffset must be set to -1 to center the map where you want it
        zoomOffset: -1,
        // Change to your access token from your mapping site.
        accessToken: 'e6af7839f94a43428e202e1290e0a2be'
    }).addTo(mymap);
  </script>

</body>
</html>
