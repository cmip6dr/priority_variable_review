# Point versus Mean

If we have a cyclic sequence of data values (e.g. values of surface temperature or orography around the equator), and these represent point values, then the interval means would typically be estimated by:

`[x]_i = 0.25*(x_i-1 + 2*x_i + x_i+1)`

If the values are means, an estimate of cell centre values can be obtained by de-convolving. 
