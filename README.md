# timezone-picker

If you're confused about the docs, sorry! I'll get it to work first and i'll update the docs when I get around to it. Just replace `$(selector).timezonepicker` with `timezonepickerinstance = new TimeZonePicker()` for now.

timezone-picker is the plugin to select and get timezone value of selected area(country) from WorldMap.

[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://opensource.org/licenses/mit-license.php)
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)]()
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/kevalbhatt/timezone-picker/issues)


### Live Demo: http://acenturyandabit.github.io/timezone-picker/
---------------------

![Imgur](https://i.imgur.com/YrGdPv2.png)

# Dependency
---------------------
NONE :))

# Installation
---------------------
### Poor man's installation
1. Clone the repo.
2. Copy `main.js` and `data.json` into your project directory.
3. Update `main.js` so it points to the right place to retrieve `data.json`.
4. Use it!

# Usage
---------------------

## Select any dom element where you want to create the map.

```js
let options={
    defaultValue: { value:"EAT", attribute: "zonename" },
    //or { value: "AUS", attribute: "country" }
    //or { value: "Asia/Calcutta", attribute: "timezone" }
    //or { value: "5.5", attribute: "offset" }
    
    //You can create custom shortcuts using the quickLink option.
    quickLink: [{
        "IST": "IST",
        "LONDON": "Europe/London",
        "LONDON2": "GB",
        "LONDON3": "GMT"
    }],
    
    quickLinkClass: "quick-class"
    
    hoverTextClass: "hover-class"
    hoverText: function(e, data){
        return (data.timezone + " (" + data.zonename + ")");
    }
    
    //Class name for the country drop-down.
    selectClass: "select-class"
    
    //Class name for the filter box container.
    filterBoxClass: "filter-class"
}
let p = new TimeZonePicker(options);
element.appendChild(p.element);
```
Set a custom value on load

If defaultValue is null then the system timezone is selected

**Output**

```html
<div class="filter-box">
    <select class="country-lov select-class"></select>
    <div class="quick-link quick-class"></div>
    <div class="hover-text"></div>
</div>
```

# Options
---------------------

| Parameter | Type | Default | Description |
| :---------|:---- |:--------|:----------- | 
| **width** | `Number` | `500` | width of map |
| **height** | `Number` | `250` | height of map |
| [**defaultValue**](#defaultvalue) | `Object` | System timezone | Set custome value on load `{ value: "EAT", attribute: "zonename" }` |
| [**quickLink**](#quicklink) | `Array<Object>` | `[{"IST": "IST","LONDON": "Europe/London"}]` | Creates shortcuts to select zone |
| [**quickLinkClass**](#quicklinkclass) | `String` | `quick-link` | quickLinkClass will be appended with the default value |
| [**filterBoxClass**](#filterboxclass) | `String` | `filter-box` | filterBoxClass will be appended with the default value |
| **selectBox** | `Boolean` | `true` | If it is set to false select box will not be created |
| [**selectClass**](#selectclass) | `String` | `country-lov` | selectClass is appended with the default value |
| **showHoverText** | `Boolean` | `true` | If it is set to false hover text will not be shown |
| [**hoverText**](#hovertext) | `Function` | `timezone(zonename)` | Called on hover of country (works only if showHoverText is true) |
| [**hoverTextClass**](#hovertextclass) | `String` | `hover-text` | hoverTextClass is appended with the default value |
| **hoverTextEl** | `Jquery selector` | `Appened in filter-box` | hover text element is appended in selector |
| **mapHoverType**  | `String` | hover polygon(area) | by default it will show hovered polygon(area) on which mouse is pointed [other hover options](#maphovertype-options) |



### mapHoverType options
| Parameter | Type | Description |
| :---------|:---- |:----------- | 
| **timezone** | `String`| when you hover on the map it will highlight all country with the same timezone
| **country** | `String`| when you hover on the map it will highlight all country with same country code |
| **zonename** | `String`| when you hover on the map it will highlight all country with the same zone name |
    

# Methods
---------------------

### .setValue(value[String-required],attribute[String-optional])

Select the value(country) based on value and attribute parameter.


* Set timezone string as a first parameter for example: 'Asia/Kolkata'.
* Default attribute is "timezone";

```js
$(selector).data('timezonePicker').setValue('Asia/Kolkata')
```

* If you want to set value based on offset then set the 1st parameter as an offset string("5.5") and 2nd parameter to 'offset'

```js
$(selector).data('timezonePicker').setValue('5.5','offset')
```

* If you want to set value based country code then set the 1st parameter as country code and 2nd parameter to 'country'

```js
$(selector).data('timezonePicker').setValue('IN','country')
```

* If you want to set value based zonename then set the 1st parameter as zonename(IST) and 2nd parameter to 'zonename'

```js
$(selector).data('timezonePicker').setValue('IST','zonename')
```

### .getValue()

It returns object containing timezone details of seleted area:

```js
$(selector).data('timezonePicker').getValue()
```

Sample returned Object

```js
  [
    {
        "selected":true,
        "zonename":"IST",
        "offset":5.5,
        "pin":"361,115",
        "country":"LK",
        "timezone": "Asia/Colombo",
    },
    {
        "zonename":"IST",
        "offset":5.5,
        "pin": "373,94",
        "country":"IN",
        "timezone": "Asia/Kolkata",
    }
]
``` 

### .getSystemTimezone()

It returns an object containing system timezone details.

### .getTimeZoneObject(value[String-required],attribute[String-optional])

It returns an object containing timezone details based on value and attribute.

* Get timezone `Object` using timezone string example: 'Asia/Kolkata'.
* Default attribute is "timezone";

```js
$(selector).data('timezonePicker').getTimeZoneObject('Asia/Kolkata');
```

* If you want to get Object based on offset then set the 1st parameter as an offset string("5.5") and 2nd parameter to 'offset'

```js
$(selector).data('timezonePicker').getTimeZoneObject('5.5','offset');
```

* If you want to get Object based country code then set the 1st parameter as country code and 2nd parameter to 'country'

```js
$(selector).data('timezonePicker').getTimeZoneObject('IN','country');
```

* If you want to get Object based zonename then set the 1st parameter as zonename(IST) and 2nd parameter to 'zonename'

```js
$(selector).data('timezonePicker').getTimeZoneObject('IST','zonename');
```

### .getZoneName(value[String-required],attribute[String-optional])

It returns an zonename based on value and attribute.

* Get zonename `String` using timezone string example: 'Asia/Kolkata'.
* Default attribute is "timezone";

```js
$(selector).data('timezonePicker').getZoneName('Asia/Kolkata');
```

* If you want to get zonename based on offset then set the 1st parameter as an offset string("5.5") and 2nd parameter to 'offset'

```js
$(selector).data('timezonePicker').getZoneName('5.5','offset');
```

* If you want to get zonename based country code then set the 1st parameter as country code and 2nd parameter to 'country'

```js
$(selector).data('timezonePicker').getZoneName('IN','country');
```


### .getTimeZoneString(value[String-required],attribute[String-optional])

It returns an timezone string based on value and attribute.

* Get timezone `String` using country code example: 'IN'.
* Default attribute is "country";

```js
$(selector).data('timezonePicker').getZoneName('IN');
```

* If you want to get timezone string based on offset then set the 1st parameter as an offset string("5.5") and 2nd parameter to 'offset'

```js
$(selector).data('timezonePicker').getTimeZoneString('5.5','offset');
```

* If you want to get timezone string based zonename then set the 1st parameter as zonename(IST) and 2nd parameter to 'zonename'

```js
$(selector).data('timezonePicker').getTimeZoneString('IST','zonename');
```

# Events
---------------------

## map:loaded

As soon as the map is loaded and ready the **map:loaded** is fired.
To catch it you can use:
```
$(selector).on("map:loaded" , function(){
    console.log("Map is loaded, have fun!");
});
```

## map:value:changed

Whenever the value of the timezone changes, the event **map:value:changed** is fired.
To catch it you can use:
```
$(selector).on("map:clicked" , function(){
    console.log($(selector).data('timezonePicker').getValue());
});
```


## map:country:clicked

Event **map:country:clicked** is fired, when a user clicks on the country.
To catch it you can use:
```
$(selector).on("map:country:clicked" , function(){
    console.log($(selector).data('timezonePicker').getValue());
});
```

## map:quickLink:clicked

Event **map:quickLink:clicked** is fired, when a user clicks on the quickLink button.
To catch it you can use:
```
$(selector).on("map:quickLink:clicked" , function(){
    console.log($(selector).data('timezonePicker').getValue());
});
```

## map:option:changed

Event **map:option:changed** is fired, when a user changes the value from the country drop-down.
To catch it you can use:
```
$(selector).on("map:option:changed" , function(){
    console.log($(selector).data('timezonePicker').getValue());
});
```

## License
---------------------
It is available under the [MIT LICENSE](LICENSE.md)
