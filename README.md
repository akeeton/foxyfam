
  <script src="https://cdn.maptiler.com/mapbox-gl-js/v0.53.0/mapbox-gl.js"></script>
  <link href="https://cdn.maptiler.com/mapbox-gl-js/v0.53.0/mapbox-gl.css" rel="stylesheet" />
  <style>
    #map {position: absolute; top: 0; right: 0; bottom: 0; left: 0;}
  </style>
<body>
  <div id="map"></div>
  <script>
    var map = new mapboxgl.Map({
      container: 'map',
      style: 'https://api.maptiler.com/maps/streets/style.json?key=4ke0chdpyxlvDiQVqDdz',
      center: [-30.15735, 33.31000],
      zoom: 2.62
    });

    map.on('load', function() {
      map.addSource('geojson-overlay', {
        'type': 'geojson',
        'data': 'https://api.maptiler.com/data/cad26d21-ffff-4bc3-9c41-7a57b9630e42/features.json?key=4ke0chdpyxlvDiQVqDdz'
      });
      map.addLayer({
        'id': 'geojson-overlay-fill',
        'type': 'fill',
        'source': 'geojson-overlay',
        'filter': ['==', '$type', 'Polygon'],
        'layout': {},
        'paint': {
          'fill-color': ['coalesce', ['get', 'fill'], '#fff'],
          'fill-opacity': 0.2
        }
      });
      map.addLayer({
        'id': 'geojson-overlay-line',
        'type': 'line',
        'source': 'geojson-overlay',
        'layout': {},
        'paint': {
          'line-color': ['coalesce', ['get', 'stroke'], 'rgb(68, 138, 255)'],
          'line-width': 3
        }
      });
      map.addLayer({
        'id': 'geojson-overlay-point',
        'type': 'circle',
        'source': 'geojson-overlay',
        'filter': ['==', '$type', 'Point'],
        'layout': {},
        'paint': {
          'circle-color': ['coalesce', ['get', 'marker-color'], 'rgb(68, 138, 255)'],
          'circle-stroke-color': '#fff',
          'circle-stroke-width': 6,
          'circle-radius': 7
        }
      });
    });
  </script>
