[![Open Source Love](https://badges.frapsoft.com/os/v2/open-source.svg?v=103)](https://github.com/ellerbrock/open-source-badges/)

# Location Picker Javascript Plugin

An open source location picker plugin written with plain javascript using Google Maps v3.

[LIVE DEMO](https://cyphercodes.github.io/location-picker/example/)

## Requirements

* Google Maps v3

## Usage

### Import libraries from HTML:

```
<link rel="stylesheet" href="../src/location-picker.css">
<script type="text/javascript" src="https://maps.googleapis.com/maps/api/js?key=AIzaSyC5Jrp9PtHe0WapppUzxbIpMDWMAcV3qE4"></script>
<script src="../src/location-picker.js"></script>
```

### Add element in HTML with a unique id:

```
#map {
    width: 100%;
    height: 480px;
}
<div id="map"></div>
```

### Initialize the LocationPicker plugin:
```
var locationPicker = LocationPicker.init('map', {
    setCurrentPosition: true, // You can omit this, defaults to true
}, {
    zoom: 15 // You can set any google map options here, zoom defaults to 15
});
```

## Methods

#### LocationPicker.init(elementId, pluginOptions, mapOptions)

Returns a reference to the LocationPicker object

#####`elementId`: 
The ID of the HTML element you want to initialize the plugin on.

##### `pluginOptions`: 

Options specific for this plugin

The only supported option for now is `setCurrentPosition` which specifies if you want the plugin to automatically try and detect and set the marker to the the current user's location _(defaults to true)_.

##### `mapOptions`:

You can set any specific google maps option here.

For a list of all the available options please visit: 

https://developers.google.com/maps/documentation/javascript/reference#MapOptions

#### LocationPicker.getMarkerPosition()

Returns an object that contains the lat and lng of the currently selected position.

## Properties

#### LocationPicker.element 

A reference to the element the plugin was initialized on.

#### LocationPicker.map

A reference to the Google Map object


## Full Example

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Location Picker Example</title>
    <link rel="stylesheet" href="../src/location-picker.css">
    <script type="text/javascript"
            src="https://maps.googleapis.com/maps/api/js?key=AIzaSyC5Jrp9PtHe0WapppUzxbIpMDWMAcV3qE4"></script>
    <script src="../src/location-picker.js"></script>

    <style type="text/css">
        #map {
            width: 100%;
            height: 480px;
        }
    </style>
</head>
<body>

<div id="map"></div>

<br>
<button id="confirmPosition">Confirm Position</button>
<br>
<p>On idle position: <span id="onIdlePositionView"></span></p>
<p>On click position: <span id="onClickPositionView"></span></p>
<script>

    // Get element references
    var confirmBtn = document.getElementById('confirmPosition');
    var onClickPositionView = document.getElementById('onClickPositionView');
    var onIdlePositionView = document.getElementById('onIdlePositionView');

    // Initialize LocationPicker plugin
    var locationPicker = LocationPicker.init('map', {
        setCurrentPosition: true, // You can omit this, defaults to true
    }, {
        zoom: 15 // You can set any google map options here, zoom defaults to 15
    });

    // Listen to button onclick event
    confirmBtn.onclick = function () {
        // Get current location and show it in HTML
        var location = locationPicker.getMarkerPosition();
        onClickPositionView.innerHTML = 'The chosen location is ' + location.lat + ',' + location.lng;
    };

    // Listen to map idle event, listening to idle event more accurate than listening to ondrag event
    google.maps.event.addListener(locationPicker.map, 'idle', function (event) {
        // Get current location and show it in HTML
        var location = locationPicker.getMarkerPosition();
        onIdlePositionView.innerHTML = 'The chosen location is ' + location.lat + ',' + location.lng;
    });
</script>
</body>
</html>
```




