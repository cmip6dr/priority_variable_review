# Overview

The C3S list from Dec. 2020 has 58 variables with 18 CMIP6 structures.

In terms of the dimensionality, there are just three combinations:

* Global, time-invariant fields on a single vertical level;
* Global, time varying fields on a single vertical level;
* Global, time varying fields on 19 pressure levels.

In the CMIP6 request, differences temporal sampling (e.g. daily versus monthly) are not considered as different structures. 

```
No temporal dimensions ... fixed field, Global field (single level) [XY-na]
No temporal dimensions ... fixed field, Global field (single level) [XY-na] [amla]
No temporal dimensions ... fixed field, Global field (single level) [XY-na] [amn-fx]
No temporal dimensions ... fixed field, Global field (single level) [XY-na] [amns-fx]
No temporal dimensions ... fixed field, Global field (single level, area sum) [XY-na]
Temporal Maximum, Global field (single level) [XY-na] {:height2m} [tmax]
Temporal Minimum, Global field (single level) [XY-na] {:height2m} [tmin]
Temporal mean, Global field (19 pressure levels) [XY-P19] [tmean]
Temporal mean, Global field (single level) [XY-na] [am-tm]
Temporal mean, Global field (single level) [XY-na] [amnla-tmn]
Temporal mean, Global field (single level) [XY-na] [amnsi-twm]
Temporal mean, Global field (single level) [XY-na] [amse-tmn]
Temporal mean, Global field (single level) [XY-na] {:height10m} [tmean]
Temporal mean, Global field (single level) [XY-na] {:height2m} [dmax]
Temporal mean, Global field (single level) [XY-na] {:height2m} [dmin]
Temporal mean, Global field (single level) [XY-na] {:height2m} [tmean]
Temporal mean, Global field (single level) [XY-na] {:sdepth1} [amnla-tmn]
Temporal weighted mean, Global field (single level) [XY-na] {:typesi} [amse-tmn]
```

The simplest file structure is for the `No temporal dimensions ... fixed field, Global field (single level) [XY-na]` case, which is used for orography, `sftlf` and `sftglf`. 

First consider a standard lat-lon grid:
```
	double lat(lat) ;
		lat:bounds = "lat_bnds" ;
		lat:units = "degrees_north" ;
		lat:axis = "Y" ;
		lat:long_name = "Latitude" ;
		lat:standard_name = "latitude" ;
	double lat_bnds(lat, bnds) ;
	double lon(lon) ;
		lon:bounds = "lon_bnds" ;
		lon:units = "degrees_east" ;
		lon:axis = "X" ;
		lon:long_name = "Longitude" ;
		lon:standard_name = "longitude" ;
	double lon_bnds(lon, bnds) ;
```

```
float ${name}(lat, lon) ;
		${name}:standard_name = "${standard_name}" ;
		${name}:long_name = "$(title}" ;
		${name}:units = "${units}" ;
		${name}:cell_methods = "area: mean";
		${name}:cell_measures = "area: areacella" ;
		${name}:missing_value = ${mv} ;
		${name}:_FillValue = ${mv} ;
```

* `cell_measures`: this is considered as part of the structure: different `cell_measures` values imply substantially different encoding;
* `cell_methods`: this string has a complex structure ... the string itself is considered as a semantic object so that we can arrive at a pragmatic 
classification of different structures.  BUT -- HAVE A SINGLE VALUE FOR THIS STRUCTURE ....

## No temporal dimensions ... fixed field, Global field (single level, area sum) [XY-na]

There are two variables with no cell measures:

```
float ${name}(lat, lon) ;
		${name}:standard_name = "${standard_name}" ;
		${name}:long_name = "$(title}" ;
		${name}:units = "${units}" ;
		${name}:cell_methods = "area: sum" ;
		${name}:missing_value = ${mv} ;
		${name}:_FillValue = ${mv} ;
```

This form is used for the `areacella` and `areacello` variables which contain the cell area. 


## No temporal dimensions ... fixed field, Global field (single level) [XY-na] [amla] 

For `mrsofc`:

```
float ${name}(lat, lon) ;
		${name}:standard_name = "${standard_name}" ;
		${name}:long_name = "$(title}" ;
		${name}:units = "${units}" ;
		${name}:cell_methods = "area: mean where ${mask_type}";
		${name}:cell_measures = "area: areacella" ;
		${name}:missing_value = ${mv} ;
		${name}:_FillValue = ${mv} ;
```

# Tripolar

The latitude and longitude are stored as a rank-2 array.


```
	float lat(y, x) ;
		lat:standard_name = "latitude" ;
		lat:long_name = "Latitude" ;
		lat:units = "degrees_north" ;
		lat:bounds = "bounds_lat" ;
	float lon(y, x) ;
		lon:standard_name = "longitude" ;
		lon:long_name = "Longitude" ;
		lon:units = "degrees_east" ;
		lon:bounds = "bounds_lon" ;
	float bounds_lon(y, x, nvertex) ;
	float bounds_lat(y, x, nvertex) ;
```
