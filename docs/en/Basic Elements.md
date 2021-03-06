## Basic Elements

In order to create your own Gio globe, let's learn some basic elements first. Below is an image describing the basic concepts in a globe.

<p align="center">
  <a><img src="https://github.com/syt123450/Gio.js/blob/master/assets/images/document/elements/all.png"/></a>
</p>


- [Surface](#surface)

    the whole surface of the globe.

- [Line](#line)

    the curve that connects two countries which related by some data. 

- [Background](#background)

    the background which behind the globe.

- [Halo](#halo)

    the circle of light around the globe.

- [Country](#country)

    the area on the surface which represents one specific country.

- [Ocean](#ocean)

    the area on the surface which represents the ocean of the earth.

- [Stats](#stats)

    the small window that monitors the performance of Three.js.

---

### Surface

<p align="center">
  <a><img src="https://github.com/syt123450/Gio.js/blob/master/assets/images/document/elements/surface.png"/></a>
</p>

The surface including [Country](#country) and [Ocean](#ocean). The default color scheme is `0xffffff`. The color scheme can be set through [configure()](#configure-api) as shown in the example below:

```
controller.configure({
	color: {
        surface: 0xff0000
    }
});
```

Or it can be changed dynamically using [setSurfaceColor()](#setSurfaceColor).


---

### Country

<p align="center">
  <a><img src="https://github.com/syt123450/Gio.js/blob/master/assets/images/document/elements/country.png"/></a>
</p>

Each Country corresponds to a specific code in [CountryData](https://github.com/syt123450/Gio.js/blob/master/src/countryInfo/CountryData.js). Depending on data availability and user activity, a Country can be in the following states:

- `Selected`

    When the user clicks on a Country, it is highlighted and becomes selected. The country is called a **selected** country.
    
	The color of Selected country can be set through [configure()]() as follows:
	```javascript
	controller.configure({
		color: {
	        selected: 0xff0000
	    }
	});
	```
	Or it can be changed dynamically with [setSelectedColor()]().

- `Related`

    Those countries connected to the selected country through 'in line' or 'out line' are called **related** countries.

	The brightness of related countries can be set through [configure()]() as follows:
	```javascript
	controller.configure({
		brightness: {
	        related: 0.8
	    }
	});
	```
	Or it can be changed dynamically with [ adjustRelatedBrightness()](). Default value: 0.5
- `Mentioned`
    
    All other countries appear in the input dataset but are not 'selected' or 'related' are called 'mentioned'.
    
	The Color of Mentioned country can be set to be brighter than Unmentioned country with [ligtenMentioned(true)](); to disable this feature use [ligtenMentioned(false)]().

	The brightness of Mentioned country can be set through [configure()] as follow:
	```javascript
	controller.configure({
		brightness: {
	        mentioned: 0.8
	    }
	});
	```
	Or it can be modified dynamically with [adjustMentionedBrightness()]() when [ligtenMentioned(true)]() is called. Default value: 0.5

- `Unmentioned`

    Countries in  [CountryData](https://github.com/syt123450/Gio.js/blob/master/src/countryInfo/CountryData.js) but not in the input data are called 'Unmentioned'.

- `Unclickable`

    When a country is set to unclickable, it will be not highlighted when clicked and it will be cause the globe to rotate. (Normally after a country has been clicked, the globe will turn and let the clicked country facing the user.).

	Unmentioned countries can be set to 'unclickable' through [disableUnmentioned(true)](#disableunmentioned). To disable this feature call [disableUnmentioned(false)](#disableunmentioned).


---

### Line

<p align="center">
  <a><img src="https://github.com/syt123450/Gio.js/blob/master/assets/images/document/elements/line.png"/></a>
</p>

Line is used to visualize the data flow between two countries. For [Selected](#country) country, the line with data flow into it is called `in line` and the line with data flow out of it is called `out line`. The default color of `in line` is ![in-line](https://placehold.it/15/154492/000000?text=+) `0x154492` and the default color of `out line` is ![out-line](https://placehold.it/15/dd380c/000000?text=+) `0xdd380c`.

The color of lines can be set through [configure API](#configure-api)  as follow:

	```javascript
	controller.configure({
		color: {
		    in: 0xff0000,
		    out: 0x00ff00
		}
	});
	```
Or it can be modified dynamically with [setInLineColor()](#setInLineColor) and [setOutLineColor()](#setOutLineColor).

Can we use different colors for different lines? The answer is yes. This can be done by modifying the json input data as follow:

```
{
	"e": "CN",
	"i": "US",
	"v": 100000,
	"inColor": "#0000ff",
	"outColor": "#00ff00"
}
```
However this needs to be done before `controller.init()` is called. See [working with data](#working-with-data) for details.
    

---

### Background

<p align="center">
  <a><img src="https://github.com/syt123450/Gio.js/blob/master/assets/images/document/elements/background.png"/></a>
</p>

The background is the area "behind" the earth. The default color of the background is ![background](https://placehold.it/15/000000/000000?text=+) `0x000000`. 

Background color can be set through [configure()](#configure-api) as follow: 

```javascript
controller.configure({
	color: {
	    background: 0x0000ff
	}
});
```
	
Or it can be modified dynamically with [setBackgroundColor()](#setbackgroundcolor).

---

### Halo

<p align="center">
  <a><img src="https://github.com/syt123450/Gio.js/blob/master/assets/images/document/elements/halo.png"/></a>
</p>

Halo is the circle of light around the earth. The default color of halo is ![halo](https://placehold.it/15/ffffff/000000?text=+) `0xffffff`. 

The color can be set through [configure()](#configure-api) as follow:
```javascript
controller.configure({
	color: {
	    halo: 0xff0000
	}
});
```
Or it can be modified dynamically by [setHaloColor()](#sethalocolor).

---

### Ocean

<p align="center">
  <a><img src="https://github.com/syt123450/Gio.js/blob/master/assets/images/document/elements/ocean.png"/></a>
</p>

The ocean object is the ocean area on the earth, the ocean is the most dart area on the earth. The default brightness of the ocean is `0.5`. 

The brightness of the ocean through [configure()]() as follow: 
```javascript
controller.configure({
	brightness: {
	    ocean: 0.8
	}
});
```
or [adjustOceanBrightness](#adjustoceanbrightness) API.

---

### Stats

<p align="center">
  <a><img src="https://github.com/syt123450/Gio.js/blob/master/assets/images/document/elements/stats.png"/></a>
</p>

The "stats" is a performance monitor for Three.js, if you are interested in it, you can see more information about stats from its [github](https://github.com/mrdoob/stats.js/). As our Gio globe is an open source library based on Three.js, so you may be want to add stats to your scene, you can use the [enableStats()](#enablestats) to add the stats panel in the left-top corner.
