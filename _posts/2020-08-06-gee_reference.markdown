---
layout: post
title:  "Google Earth Engine reference sheet"
author: Mint
date:   2020-08-06
category: Google Earth Engine
keywords: Quick look-up
abstract: "Iteration, Get border images, Advance date, date stuff, Export image, ..."
---

* * * 

##### Iteration/for loop equivalent

It's not a good idea to use a for loop, so we do this instead

Stack exchange link: [https://gis.stackexchange.com/questions/291121/gee-hangs-in-a-for-loop-using-dates](https://gis.stackexchange.com/questions/291121/gee-hangs-in-a-for-loop-using-dates)

link: [https://code.earthengine.google.com/a9ea948e1f3b3419f3f41c9a315a72dc](https://code.earthengine.google.com/a9ea948e1f3b3419f3f41c9a315a72dc)

    var changingDate = ee.Date.fromYMD(2019, 01, 01);
    var listVariable = ee.List.sequence(0, 81);
    var datesList = listVariable.map(function(d) {
    var currentDate = changingDate.advance(d, 'week'); 
    return currentDate.get('week');
    });
    print(datesList);

* * * 

##### Get borders images

The desired border is obtained from a vector dataset. [Click here](https://developers.google.com/earth-engine/vector_datasets) for Google Earth Engine's selected vector datasets catalog

link example 1: (https://code.earthengine.google.com/051055ee1b2dab3e64934205852f4a18)[https://code.earthengine.google.com/051055ee1b2dab3e64934205852f4a18]

link example 2: (https://code.earthengine.google.com/410805d94e9c87bda3ce895efee77ade)[https://code.earthengine.google.com/410805d94e9c87bda3ce895efee77ade]

    // declare a region polygon
    var polygon = ee.Geometry.Polygon([
    [[-128, 23], [-63, 23], [-63, 50], [-128, 50], [-128, 23]]
    ]);

    // This data set contains US boundaries. Other datasets may need
    // filtering
    var dataset = ee.FeatureCollection('TIGER/2018/States');

    // Set the style of the line work
    var styleParams = {
    // fill color is in format HHHHHHAA where H is
    // regular hexadecimal color and AA is the opacity
    fillColor: 'b5ffb400',
    color: '000000', // color of the line
    width: 3.0, // width of the line
    };

    // Get the desired image by filtering our dataset by style
    var image = dataset.style(styleParams);

    // Create thumbnail characteristics
    var thumbArgs = {
    'region': polygon, // region from polygon
    'dimensions': 1000, // dimensions
    'crs': 'EPSG:3857' // just copy this in for looking right
    };

    // Create the thumbnail URL
    var thumbnail = image.getThumbURL(thumbArgs);
    print('Main US', thumbnail); // display thumbnail in a link

    print(ui.Thumbnail(image, thumbArgs)); // display in Console


* * *

##### Advance date by a day/week/month/etc

link: [https://code.earthengine.google.com/39eee0c9c68f9f0ab45d8e08a72e2770](https://code.earthengine.google.com/39eee0c9c68f9f0ab45d8e08a72e2770)


    var myDate = ee.Date('2020-03-01');
    print(myDate);
    myDate = myDate.advance(1, 'week');
    print(myDate);

* * * 

##### Get date year/month/week/day

link: [https://code.earthengine.google.com/647cd492e5a0ccc1cebd8bde8476c169](https://code.earthengine.google.com/647cd492e5a0ccc1cebd8bde8476c169)

    var myDate = ee.Date.fromYMD(2020,12,21);
    print(myDate.get('week'));

* * * 

##### Get image:

link: [https://code.earthengine.google.com/5f6a68b8ca324e9980e9546e743a097d](https://code.earthengine.google.com/5f6a68b8ca324e9980e9546e743a097d)
    
    // These are the geometries
    var MainUS = /* color: #0b4a8b */ee.Geometry.Polygon(
    [[[-125.2189022974363, 39.87625675657812],
    [-119.9454647974363, 33.541652433680305],
    [-117.4845272974363, 32.80600467030436],
    [-110.9806210474363, 31.46641749852086],
    [-108.5196835474363, 31.316365588865388],
    [-101.8399960474363, 29.80278626477314],
    [-99.7306210474363, 26.86355651435467],
    [-97.4454647974363, 26.234579437417167],
    [-96.0392147974363, 28.11102154050461],
    [-84.26187104743632, 29.955202498828807],
    [-81.09780854743632, 24.966420522552227],
    [-79.33999604743632, 25.60218115809836],
    [-80.21890229743632, 31.316365588865388],
    [-66.33218354743632, 43.0370019010403],
    [-68.79312104743632, 46.89044292169136],
    [-72.30874604743632, 45.306020109394304],
    [-81.62515229743632, 41.73875923671617],
    [-82.85562104743632, 42.26127804228795],
    [-82.85562104743632, 45.92080248327908],
    [-123.4610897974363, 49.23932274975353],
    [-123.6368710474363, 48.312633583457036],
    [-125.7462460474363, 48.312633583457036]]]),
    Hawaii = 
    /* color: #bf04c2 */
    /* shown: false */
    ee.Geometry.Polygon(
    [[[-166.38904585479986, 15.353499540242268],
    [-152.32654585479986, 18.714327031280035],
    [-153.90857710479986, 25.071086607110242],
    [-166.21326460479986, 26.652776484972765],
    [-170.60779585479986, 23.30736558401026]]]),
    Alaska = 
    /* color: #ff0000 */
    /* shown: false */
    ee.Geometry.Polygon(
    [[[-141.31373618243083, 60.64018250178644],
    [-141.31373618243083, 70.53174986100197],
    [-147.99342368243083, 71.10919966082687],
    [-155.37623618243083, 71.67012908693061],
    [-164.51686118243083, 71.4477127226392],
    [-167.32936118243083, 69.0759061112182],
    [-168.38404868243083, 67.24601397933378],
    [-170.84498618243083, 64.6703138328161],
    [-175.76686118243083, 60.98308042548612],
    [-172.60279868243083, 51.24727729555947],
    [-158.54029868243083, 53.604704382683884],
    [-144.12623618243083, 54.01984811098307],
    [-133.93092368243083, 54.63487820624491],
    [-130.06373618243083, 55.837518825089646],
    [-135.68873618243083, 60.11891380256326]]]);

    var collection = ee.ImageCollection('COPERNICUS/S5P/NRTI/L3_NO2')
    .select('NO2_column_number_density')
    .filterDate('2020-03-01', '2020-03-06');

    var image = collection.mean();

    var thumbnail1 = image.getThumbURL({
    min: 0,
    max: 0.0002,
    palette: ['black', 'blue', 'purple', 'cyan', 'green', 'yellow', 'red'],
    'region': MainUS,
    'dimensions': 500,
    'crs': 'EPSG:3857'
    });
    print('Main US', thumbnail1);


    var thumbnail2 = image.getThumbURL({
    min: 0,
    max: 0.0002,
    palette: ['black', 'blue', 'purple', 'cyan', 'green', 'yellow', 'red'],
    'region': Alaska, 
    'dimensions': 500,
    'crs': 'EPSG:3857'
    });
    print('Alaska', thumbnail2);


    var thumbnail3 = image.getThumbURL({
    min: 0,
    max: 0.0002,
    palette: ['black', 'blue', 'purple', 'cyan', 'green', 'yellow', 'red'],
    'region': Hawaii,
    'dimensions': 500,
    'crs': 'EPSG:3857'
    });
    print('Hawaii', thumbnail3);


* * *
