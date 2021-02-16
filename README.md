# BlueCity_Aggregated_HTTP_API
Aggregated traffic information can be downloaded from BlueCity database using simple HTTP requests. 

# BlueCity_Aggregated_HTTP_API
Aggregated traffic information can be downloaded from BlueCity database using simple HTTP requests. 

Introduction to IndiGO IQ APIs
IndiGO IQ provides different levels of access to data generated by our sensors and platform. 
This document provides instructions on how to use our API. 

Real-Time API:
This API provides access to the location, class, and tracking ID of each object within a frame. This API can be used to build more advanced applications on top of our traffic monitoring solution. 
The WebSocket library was built in python for your convenience. You can either use this library or make the communication from scratch by yourself. 

The expected outputs of API are:

•	The timestamp of the frame,

•	Class of all objects followed by:

•	Tracking ID associated with each object

•	Coordination of the object with respect to the sensor's location

•	Width and length of the object

For each call of the API, the following rules should be satisfied:

The URL of the service is "wss://realtime.bluecitytechnology.com/ws/realtime/{UDID}/"

Please fill the {UDID} with your devices' UDID. 

NOTE: We can offer a demo UDID to test API with one of the existing sensors: BCT_3D_5G_0101002. 

NOTE: Please contact us to request a test Token

You need to add the token and UDID of the device in the header of the request. 

headers={"token": "YOUR_TOKEN", "UDID": "BCT_3D_5G_0101001"} 

We provide a free Python (Version 3.7) library that you can use to ease this process. The API will be running on a separate process that won't block your current process. You can click on this link to download the library. The following instructions can be followed to use the library:

1.	Create an object from BCTWSConnection class. You only need to pass two UDID and token arguments to it. Like this: 
 c= BCTWSConnection("BCT_3D_5G_0101001", "YOUR_TOKEN")
 
2.	Call the "get" function to receive a frame.  frame = c.get()

You can find an example in the main section of the provided module. The format of frames is based on the following structure.
Structure:

timestamp, objectId_1, centerX_1, centerY_1, width_1, length_1, classType_1, accuracy_1,angle_1,speed_1, objectId_2, centerX_2, centerY_2, width_2, length_2, classType_2, accuracy_2,angle_2,speed_2,<End of the frame token>

A sample output: 
2018-01-02T22:10:05.284208,O1,123,124,5,22,1,99.9,256,25,O2,256,457,124,20,2,85.2,23,22,<EOF>

Notes:
•	The structure and the sample are color-coded for better understanding. 
•	The timestamp is based on the ISO 8601 format.
•	The classType of a detected object can be either

	0: Pedestrians (old version)
  
	1: Vehicles (old version)
  
	2: Car
  
	3: Van
  
	4: Truck
  
	5: Bus
  
	6: SUV
  
	7: Construction_vehicle
  
	8: Trailer
  
	9: Tractor
  
	10: Pedestrian
  
	11: Person_sitting
  
	12: Cyclist
  
	13: Bicycle
  
	14: Person
  
	15: Motorcycle
  
	16: Rollerblader
  
	17: Cyclists
  
•	The object ID of a single detected object will be consistent in all of the frames that the object appears.

•	This API can be offered using MQTT Protocol upon the existence of a Broker Network. 

Aggregated HTTP API:
Aggregated traffic information can be downloaded from our database using simple HTTP requests. This section provides details on how to use this API. 

The URL of the service is: https://api.bluecitytechnology.com/s/ad
The request type should be a GET request.
The parameters require assigning a value to them:

•	UDID: ID of the sensor

•	fdate: starting date of the requested date-time range (in ISO 8601 format)

•	tdate ending  date of the requested date-time range (in ISO 8601 format) 

•	f: fields that you desire to get the values (fields should be separated by commas)

•	a: the type of aggregation 

•	simplified: for simplified output, it should be 1 otherwise 0 (recommend to use the simplified output)

Parameters details are based on the following information.

•	The UDID of devices, You can use BCT_3D_5G_0101001 as a demo UDID

•	For the field properties, you can use the following keywords separated by commas.

	ne (vehicle movements - north to east)
  
	ns (vehicle movements - north to south)
  
	nw (vehicle movements - north to west)
  
	es (vehicle movements - east to south)
  
	ew (vehicle movements - east to west)
  
	en (vehicle movements - east to north)
  
	sw (vehicle movements - south to west)
  
	sn (vehicle movements - south to north)
  
	se (vehicle movements - south to east)
  
	wn (vehicle movements - west to north)
  
	we (vehicle movements - west to east)
  
	ws (vehicle movements - west to south)
  
	nrl (pedestrian movements right to left -  north crosswalk)
  
	nlr (pedestrian movements left to right -  north crosswalk)
  
	erl (pedestrian movements right to left -  east crosswalk)
  
	elr (pedestrian movements left to right -  east crosswalk)
  
	srl (pedestrian movements right to left -  south crosswalk)
  
	slr (pedestrian movements left to right -  south crosswalk)
  
	wrl (pedestrian movements right to left -  west crosswalk)
  
	wlr (pedestrian movements left to right -  west crosswalk)
  
•	For the aggregation field, please use one of the following values:
	
        1: 15 minutes
  
	2: Hourly
  
	3: Daily
  
	4: Monthly
  
•	Also, please provide the date fields with ISO 8601 format like the following example:
2020-06-30T10:00:42

Here is an example request:
https://api.bluecitytechnology.com/s/ad?UDID=BCT_3D_5G_0101002&fdate=2020-06-30T10:00:42&tdate=2020-06-30T15:00:42&f=ne,nw,ns,nlr,nrl,&a=2&simplified=1

Please request a demo Token to test our APIs.
All APIs will be upgrading consciously with more classes of road users and traffic data/analytics. 
Other traffic data still will be available through our IndiGO iQ dashboard.
