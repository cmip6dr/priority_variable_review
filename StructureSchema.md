# Structure Schema

CMIP6: 

* Title, Label, ID, description
* Spatial shape, temporal shape, cell methods
* Coordinates
* Other dimensions
* cell measures
* flag values, flag meanings, prov, processing note

Revision
The cell measures is essentially an aspect of the spatial shape. 
Flag values and flag meanings: used very little .. make more sense as part of the CMOR variable.
prov, processing note: should be in a structure

Cell methods includes information on masking, averaging, etc which is related to the specification of the variables. 

Coordinate information which is an extension of the parameter definiton, and really belongs in the CMOR variables. 

If we consider cell methods, coordinates, flag values and flag meanings as external to structures, then the 220 CMIP6 structure records reduces to 85 structures in the new schema.

However, we do wish to distinguish between cell data and point data. Cell data may be the mean, sum, maximum, minimum etc over a cell, but the common requirements is that bounds be specified. The spatial data is always considered as cell data. Temporal data can be taken as purely point data.

The proposal is to have a functional approach to dealing with cell methods, so that it is possible to pick apart the different elements. 

There are a number of CMIP6 cell methods strings which make no reference to spatial processing: these should be modified. The default interpretation when it is omitted is specified by the CF Convention and depends on the nature of the data variable, it defaults to `mean` for extensive parameters and `point` for intensive ones ((http://cfconventions.org/cf-conventions/cf-conventions.html#cell-methods)[Section 7.3]). Another way of looking at this is that if it makes a sense as a point value, that is the default.

* `time: mean` : four Calipso-simulator cloud cover parameters, `area: mean`.
* `time: mean` : one ocean transect varaible: `sum` along transect, which is not an explicit dimension [need to look into this].

