# Storymaps

This package generates a 3D city using geojson data from OpenStreetMaps, generated by overpass-turbo.

## Before Installation

Get the geojson data from [overpass-turbo](https://overpass-turbo.eu);

Select the area you want to display on the website, and copy and run the query below.
Click on Export and save as geojson.

```
[out:json]
[bbox:{{bbox}}]
[timeout:30];

(

way["building"]({{bbox}});
relation["building"]["type"="multipolygon"]({{bbox}});

way["highway"]({{bbox}});
relation["highway"]["type"="polygon"]({{bbox}});

way["natural"="water"]({{bbox}});
way["water"="lake"]({{bbox}});
way["natural"="coastline"]({{bbox}});
way["waterway"="riverbank"]({{bbox}});
);

out;
>;
out qt;
```

You also need the latitude and longitude coordinates of the center of the selected area.
You can use Google Maps to get this data.

## Installation & Setup

install the package using npm

```
npm install storymaps
```

Then, import it in your javascript, create a configuration and start the setup.

data: path to your geojson

path: change after setup

container: the id of the div where you want to place the canvas

citycenter: array of [longitude, latitude] of the center of your area

```
import * as storymaps from "./js/storymaps";

storymaps.global.config = {
	debug: true,
	data: "./data/bruges-complete.geojson",
	path: "./data/path.json",
	container: "container",
	citycenter: [3.227183, 51.209651],
	color_background: 0x222222,
	color_buildings: 0xfafafa,
	grid: { primary: 0x555555, secondary: 0x333333 },
	color_ground: 0x00ff00,
	opacity_ground: 0.25,
};

storymaps.setup();
```

This will run the map in setup mode, so you can draw the path you want to animate.
Start drawing by pressing "S" and finish and save the path by pressing "F".

Update the path to the path in the configuration.

Then stop the setup and start storymaps.

```
// storymaps.setup();
storymaps.start();
```
