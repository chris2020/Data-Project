#Project Title

######Data Representation and Querying Project 2015

#Name

######Christy Madden

#Introduction

This project is using the dataset 'Galway City Parking Locations' which can be found at the following url https://data.gov.ie/dataset/galway-city-car-parking-locations. The design and documentation for the dataset is below.

#About the dataset

The dataset is originally in the CSV (comma separated values) format and is formatted into json. The dataset can be found and downloaded from https://data.gov.ie/dataset/galway-city-car-parking-locations/resource/d967950d-faab-45ad-815d-211c9bcfb38e.

The dataset has 17 rows and covers all public car parks in the city. This dataset will continue to grow as it is expanded to to cover the surrounding areas of Galway City. 

The dataset contains 12 fields which includes different grid systems for locating the car parks.
The first 2 fields are an older coordinates system and may not be of use to you, we recommend you ignore these and choose one of the more up to date coordinate systems

*Out of date fields*

|  X |  Y |
|---|---|

*Recommended fields to use*

|OBJECTID|NAME|TYPE|NO_SPACES|LAT|LONG|EastITM|NorthITM|EastIG|NorthIG|   
|---|---|---|---|---|---|---|---|---|---|

**Note on what type of information will be retrieved with each field**

1. X: -9.053499750875776
2. Y: 53.273082469830108
3. OBJECTID: 1
4. NAME: Market St
5. TYPE: Pay/Surface Carpark, Multistorey Carpark, Surface Carpark (free parking)
6. NO_SPACES: 88
7. LAT: 53.273
8. LONG: -9.054
9. EastITM: 529691.955
10. NorthITM: 725294.803
11. EastIG: 129726.012
12. NorthIG: 225265.639

*For those who need more inforamtion about the different coordinate systems check out the links below*

[Lat & Long](https://www.learner.org/jnorth/tm/LongitudeIntro.html)

[ITM](https://en.wikipedia.org/wiki/Irish_Transverse_Mercator)

[IG](https://en.wikipedia.org/wiki/Irish_grid_reference_system)

---

####/Retrieve

######URL Structure 

    carpark_api/retrieve?field=[field]&limit[limit]

######Method

GET 

######Arguments 

|Argument|Description|
|---|---|
| field |  *The name of the fields you want. (Use ‘all’ to retrieve all fields for the row)* **E.G field=all**|
|limit| *The number of rows you want returned (defaults to 20)* **E.G limit=5**|

######Returns

Car Park information in JSON format

######Sample Response

```javascript
[{type: "Multistorey Carpark", no_spaces: 88}, {type: "Pay/Surface Carpark", no_spaces: 100}]
```

---

####/Add

######URL Structure 

    carpark_api/add?
    
######Method

POST

######Arguments

|Argument|Description|
|---|---|
| X |  *The long version of the latitute coordinates*|
|Y| *long version of the longtitute coordinates*|
| Objectid |  *The id number of the row.*|
|Name| *The name of the carpark*|
| Type |  *The type of carpark*|
|No_Spaces| *The number of spces in the carpark*|
| Lat |  *The latitude of the carpark*|
|Long| *The longtitutde of the carpar*|
| Eastitm |  *The east ITM coordinates*|
|Northitm| *The north ITM coordinates*|
| Eastig |  *The east IG coordinates*|
|Northig| *The north IG coordinates*|

*These fields must be sent in the body of the request*

######Returns

Returns a JSON object with a success value stating whether your post worked or not and shows the values paired with the fields you wanted

```javascript
{success: true, objectid : 18, name: "galway carpark", type: "multistorey carpark"}
```

######Sample Response

```javascript
{X; 1.87654, 
 Y: 2.45986, 
 objectid : 20, 
 name: "shop street carpark", 
 type: "multistorey carpark",
 No_spaces: 100,
 Lat: 1.877,
 Long: 2.60,
 Eastitm: 1498.987
 Northitm: 2193.564
 Eastig: 298764.18,
 Northig: 3981.87
 }
```

---

####/Update

######URL Structure 

    carpark_api/update?objectid=[id number]&field=[field]&values=[value]
    
######Method

PUT

######Arguments

|Argument|Description|
|---|---|
| objectid  |  *The number of the row you want to change*|
|field | *The name of the fields you want to change*|
|value  | *The values for the new field*|

*Multiple fields for the row can be changed in one go. Add a comma between fields and make sure you have the correct values for them also separated by a comma*

######Returns

Returns a JSON object with a success value stating whether your update worked or not and shows the new values paired with the fields you wanted.

######Sample Response

```javascript
{success: true, objectid : 7, name: “city center carpark”, type: “Surface Carpark (free parking)”}
```

---

####/Delete

######URL Structure

     carpark_api/delete?objectid=[id number]
     
######Method

DELETE 

######Arguments

|Argument|Description|
|---|---|
| id number  |  *The number of the row you want to delete*|

*Only full rows can be deleted, when you choose the row using the objectid all in information connected to this row will be deleted*

######Returns

A JSON object with a delete value saying whether or not it worked and the number of the row that was deleted

######Sample Response

```javascript
{Deleted: true, objectid : 9}
```







