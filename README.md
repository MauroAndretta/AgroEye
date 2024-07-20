# AgroEye
AgroEye is an innovative project focused on leveraging computer vision technology to enhance precision agriculture. By using advanced image processing and machine learning algorithms, AgroEye aims to provide farmers with real-time insights into their crops' health, growth patterns, and potential issues.
 
## Code directory
 
```
└── `AgroEye`
    ├── `conda`: conda environments
    ├── `images`: All the images, if any
    ├── `notebooks`: All notebooks such as Jupyter notebooks, if any
    ├── `src`: Python code for the app
    ├── `tests`: performance, unit and end-to-end tests
    ├── `.gitignore`
    └── `README.md`
```


## Historical Weather Data Acquisition

### Overview

The acquisition of historical weather data is the first step in conducting smart analysis on crop fields. Weather data can be correlated with satellite and drone image information to provide a comprehensive understanding of crop health and growth patterns.

### Data Collection

Currently, we obtain historical weather information for two specified dates. This data includes key weather parameters such as temperature, humidity, wind speed and total precipitation collected on both a daily and hourly basis.

### Visualizations

#### Hourly Weather Information Plot

The following plot displays the hourly temperature, humidity, wind speed and total precipitation from the specified dates:

<img src="images/weather_forecast_hourly.png" width="600" alt="Hourly Weather Information">


#### Hourly Weather Information Plot

The following plot displays the daily min and max temperature, humidity, wind speed and total precipitation from the specified dates:

<img src="images/weather_forecast_daily.png" width="600" alt="Hourly Weather Information">


## Calculate Crop Metrics from Sentinel-2 Images with Python API
 
Before computing the crop analysis is necessary to acuquire the satellite images. First of all the user must insert an existing valid address (otherwise we cannot conduct the analysis), for exaple "*Rome, Italy*" in the geocoding function, which outputs the latitude and longitude of the address. Thanks to those informaiton is possible to instanciate a `geemap.Map` object, which will be our base for the identification of the field, on which the analysis we'll be carried out. 

Once the Map is created, it is necessary to create a Polygon inside the map, using the predefined widget in the left panel of the Map:

![Capture Polygon](./images/Capture_Drawn_Polygon.PNG)

The user can create as many Polygon as she wants. All the Polygons we'll be the crops, on which the analysis we'll be condcuted. Now is it possible to acquire the satellite images from *Sentinel-2*.

```
# Filter Sentinel-2 image collection
try:
    sentinel_images = (
        ee.ImageCollection("COPERNICUS/S2_SR_HARMONIZED")
        .filterDate(start_date, end_date)
        .filterBounds(combined_geometry)
        .filter(ee.Filter.lt("CLOUDY_PIXEL_PERCENTAGE", 20))
    )
    print("Sentinel-2 images acquired correctly!")

except Exception as e:
    print("An error occurred while trying to acquire the Sentinel-2 images.")
    print(f"Error: {e}")
```

With the images correclty acquired (filtered by the `"CLOUDY_PIXEL_PERCENTAGE"`, in order to keep only noiseless information), is it possible to compute to compute all the crop metrics. 

### NDVI
The Normalized Difference Vegetation Index (NDVI) is a simple graphical indicator that can be used to analyze remote sensing measurements, typically, but not necessarily, from a space platform, and assess whether the target being observed contains live green vegetation or not.

NDVI value ranges between -1.0 and +1.0. Generally speaking, NDVI shows a functional relationship with vegetation properties (e.g. biomass). NDVI is directly related to the photosynthetic capacity and energy absorption of plant canopies. The NDVI is calculated from these individual measurements as follows:

`NDVI= (NIR-Red) \ (NIR+Red)`

The figure below show an example of NDVI index, computed for the Polygon of interest. 

![Capture Polygon](./images/NDVI_Crop.PNG)
 
## Contacts
**Build:** (mauo.andretta222@gmail.com)
 
**Ownership:** (mauo.andretta222@gmail.com)
 
**Maintenance:** 
Support & Ops (mauo.andretta222@gmail.com)

Feel free to contribute to the project!
