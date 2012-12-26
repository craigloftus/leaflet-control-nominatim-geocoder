Leaflet Control Nominatim Geocoder
=============================

# What is it ?
A simple geocoder that uses Nominatim to locate places.

# How to use it ?
```javascript
var cloudmadeAttribution = 'Map data &copy; 2011 OpenStreetMap contributors, Imagery &copy; 2011 CloudMade',
    cloudmade = new L.TileLayer('http://{s}.tile.cloudmade.com/BC9A493B41014CAABB98F0471D759707/997/256/{z}/{x}/{y}.png', {attribution: cloudmadeAttribution});

var map = new L.Map('map').addLayer(cloudmade).setView(new L.LatLng(48.5, 2.5), 15);

var geocoder = new L.Control.NominatimGeocoder();

map.addControl(geocoder);
```

# What are the options ?
You can specify an options object as a second argument of L.Control.NominatimGeocoder.
```javascript
var options = {
    collapsed: true, /* Whether its collapsed or not */
    position: 'topright', /* The position of the control */
    text: 'Locate', /* The text of the submit button */
    callback: function (results) {
        // Check if no results are returned
        if (results.length >= 1) {
            // Just take the first place
            var bbox = results[0].boundingbox,
                southWest = new L.LatLng(bbox[0], bbox[2]),
                northEast = new L.LatLng(bbox[1], bbox[3]),
                bounds = new L.LatLngBounds(southWest, northEast);
            // Center on it
            this._map.fitBounds(bounds);
        }
        // TODO Indicate lack of results to user
    }
};
```
