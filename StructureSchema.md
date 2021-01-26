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

If we consider cell methods, coordinates, flag values and flag meanings as external to structures, then the 220 CMIP6 structure records reduces to 85 structures in teh new schema.

