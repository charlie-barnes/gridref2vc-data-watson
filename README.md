# gridref2vc-data
Data to convert grid references to vice-counties

This repository contains CSV files that can be used to convert grid references to vice-counties. The data can not be used "as is", via a simple lookup. In order to reduce the size of the data files, a hierarchical system has been implemented whereby if a grid square is entirely within one vice-county, all "child" grid squares are omitted. Thus, in order to retrieve the correct conversion, if the grid square doesn't exist in the data, you need to test the "parent" grid reference.

As an example, grid square TF135384 does not exist in the data files because it's "grandparent" (its "parent", TF13 is also absent) is entirely within vice-county 53. When traversing the hierachy, you must test in the following order 100m > 1km > 2km > 10km > 100km, ignoring the 5km grid square as this does not entirely contain any "child" grid squares.

Psuedocode:
```
input = TF135384

if exists input then
  return vc(input)
else
  if exists convert_to_100m(input) then
    return vc(convert_to_100m(input))
  else
    if exists convert_to_1km(input) then
      return vc(convert_to_1km(input))
    else
      if exists convert_to_2km(input) then
        return vc(convert_to_2km(input))
      else
        if exists convert_to_10km(input) then
          return vc(convert_to_10km(input))
        else
          if exists convert_to_100km(input) then
            return vc(convert_to_100km(input))
          else
            return "invalid input"
```
It should be possible to traverse the hierachy and return a value for all valid grid references; otherwise an error indicates an invalid grid reference. The sea (where no vice-county exists but it is within the grid) is assigned a value of 0 in the data.

For working example code on how to use the data, see https://github.com/charlie-barnes/gridref2vc-examples/

For more information on vice-counties see https://en.wikipedia.org/wiki/Vice-county

The data has been generated from the NBN vice-county boundaries (Contains public sector information licensed under the Open Government Licence v3.0.) and the dataset of Irish vice-counties produced by SK53 sourced from OpenStreetMap @ https://github.com/SK53/Irish-Vice-Counties.
