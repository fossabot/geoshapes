# :books: geoshapes Library
[![PyPI version](https://badge.fury.io/py/geoshapes.svg)](https://badge.fury.io/py/geoshapes)
[![Build Status](https://app.travis-ci.com/abiraihan/geoshapes.svg?branch=master)](https://app.travis-ci.com/abiraihan/geoshapes)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/abiraihan/geoshapes/master)
[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5559438.svg)](https://doi.org/10.5281/zenodo.5559438)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fabiraihan%2Fgeoshapes.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fabiraihan%2Fgeoshapes?ref=badge_shield)

:memo: Experimental design for geospatial analytics.
To split Polygon geometry into different shape that required to create
experimental plot / trial design. It creates experimental
plot design to summerize data to geospatially enabled space for next-step
mathematical modelling.


### Run example code on mybinder.org
:pen: You can run geoshapes example code on [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/abiraihan/geoshapes/master) without installing any library in your python environment.
It doesn't requie any dependency to install and you can run all those example from the mybinder.org


#### :books: **<a href="./docs/usage.rst">Required Library</a> :arrow_forward: Required python library prior to install geoshapes**

### Install geoshapes
```python
pip install geoshapes
```

### Module Summery:

- [x]  **<a href="./docs/splitShape.rst">geoshapes.splitShape</a> :arrow_forward: Splits geometry :arrow_forward: :notebook: <a href="./example/splitShape.ipynb">See Tutorials on splitShape</a>**
- [x]  **<a href="./docs/checkShape.rst">geoshapes.checkShape</a> :arrow_forward: Check geometry validity**
- [x]  **<a href="./docs/gridShape.rst">geoshapes.gridShape</a> :arrow_forward: Create grid for geometry :arrow_forward: :notebook: <a href="./example/gridShape.ipynb">See Tutorials on gridShape</a>**
- [x]  **<a href="./docs/mergeShape.rst">geoshapes.mergeShape</a> :arrow_forward: Merge splited geometry :arrow_forward: :notebook: <a href="./example/mergeShape.ipynb">See Tutorials on mergeShape</a>**
- [ ]   **geoshapes.selectGeom :arrow_forward: Check geometry shapes and store values**
- [ ]   **geoshapes.utils :arrow_forward: Check geometry type, merge multiple dataframe and delete duplicate geometry**


## :pencil2: Example
### :earth_asia: geoshapes.splitShape.splitCircle
#### :arrow_forward: Split a circle geometry with defined indentifier as a treatment plot
```python
import string, shapely, geoshapes, geopandas
pointLocation = shapely.geometry.Point(0,0)
polygonList = geoshapes.splitShape.splitCircle(
    geoms = pointLocation,
    circleRadius = 500,
    incrementDegree = 45,
    clipInterior = True,
    innerWidth = 100,
    getGeom = 'Both'
    )
gdf = geopandas.GeoDataFrame(
    geometry = polygonList,
    crs = 'EPSG:3857'
    )
gdf['ids'] = range(len(gdf))
gdf['Group']= gdf.apply(
    lambda row : string.ascii_uppercase[int(row.ids)],
    axis = 1)
ax = gdf.plot(figsize=(15, 10),
alpha=0.0, edgecolor='k')
gdf.plot(column='Group',
         ax=ax, linewidth=9,
         cmap='tab20');
gdf.apply(lambda x: ax.annotate(
    text=f"Group : {x.Group}{x.ids}",
    xy=x.geometry.centroid.coords[0],
    weight='bold', ha='center',
    va='center', size=10),axis=1
    )
```

### :world_map: splitsCircle

![Split CIrcle](https://github.com/abiraihan/geoshapes/blob/master/docs/images/splitCircle.png?style-centerme)
_____



### :earth_asia: geoshapes.splitShape.splitLatin
#### :arrow_forward: Split a square geometry with defined indentifier as a latin square treatment plot
```python
import string, shapely, geoshapes, geopandas
point = shapely.geometry.Point(0,0)
latinShpae = geoshapes.splitShape.splitLatin(point, 25)
featureGeoms = geopandas.GeoDataFrame(
    geometry = latinShpae,
    crs = 'EPSG:4326'
    )
featureGeoms['ids'] = range(len(featureGeoms))
featureGeoms['Group']= featureGeoms.apply(
    lambda row : string.ascii_uppercase[int(row.ids)],
    axis = 1
    )
ax = featureGeoms.plot(
    figsize=(15, 10),
    alpha=0.4, edgecolor='k')
featureGeoms.plot(
    column='Group', ax=ax,
    linewidth=9, cmap='tab20'
    );
featureGeoms.apply(
    lambda x: ax.annotate(
        text=f"{x.Group}",
        xy=x.geometry.centroid.coords[0],
        ha='center',
        va='center',
        size=20),axis=1
    )
```

### :world_map: splitLatin

![Latin Square](https://github.com/abiraihan/geoshapes/blob/master/docs/images/latinSquare.png)
_____


License
----
MIT


## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fabiraihan%2Fgeoshapes.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fabiraihan%2Fgeoshapes?ref=badge_large)