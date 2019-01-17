# gridref2vc-data
Data to convert Ordnance Survey grid references to vice-counties

This repository contains data that can be used to convert grid references to vice-counties. The data can not be used "as is". In order to reduce the size of the data files, a hierarchical system has been implemented whereby if a grid square is entirely within one vice-county, all "child" grid squares are omitted. Thus, in order to retrieve the correct conversion, if the grid square doesn't exist in the data, you need to test the "parent" grid reference.

As an example, grid square TF135384 does not exist in the data files because it's "grandparent" (it's "parent", TF13 is also absent) is entirely within vice-county 53. When traversing the hierachy, you must test in the following order 1m > 10m > 100m > 1km > 2km > 10km > 100km, ignoring the 5km grid square as this does not entirely contain any "child" grid squares.

For examples on how to use the data, see https://github.com/charlie-barnes/gridref2vc-examples/

The data is based on NBN vice-county boundaries. Contains OS data © Crown copyright and database right 2018.
