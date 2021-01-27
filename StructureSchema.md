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

There are a number of CMIP6 cell methods strings which make no reference to spatial processing: these should be modified. The default interpretation when it is omitted is specified by the CF Convention and depends on the nature of the data variable, it defaults to `mean` for extensive parameters and `point` for intensive ones ([Section 7.3](http://cfconventions.org/cf-conventions/cf-conventions.html#cell-methods)). Another way of looking at this is that if it makes a sense as a point value, that is the default.

There are no explict requests for `area: point time: mean` data in the request, but there are a few for `area: time: point`. 

## Time mean

With current cell methods `time: mean`.

* Four Calipso-simulator cloud cover parameters, `area: mean`.
* One ocean transect varaible (`mfo` ) and 3 sea-ice variables: `sum` along transect, which is not an explicit dimension [need to look into this].
* Pressure level variables (e.g. `ua` on 8 pressure levels): the CF default interpretation would be as point variables, but it is not clear whether this is intended.
* Ocean model variables: these appear to be intensive (e.g. salinity). Griffies et al. indicate that, for instance, mass of salt in a cell should be computed as the mass in the cell multiplied by the reported salinity value, impying that salinity is intended to be a cell mean. This is not the default CF interpretation, so we require clarification and a probable change to `area: height: time: mean` or `volume: time: mean`.
* Four surface stress variables: intensive by default, but probably intended as exensive.
* Two sea ice mass flux variables: would make sense to consider these as mean along the gird boundary (need confirmation from SIMIP).

