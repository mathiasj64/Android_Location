# Android Location

For an application to have permission to get the location from a device we will need to require the following permissions in the AndroidManifest.xml file.

```<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.INTERNET" />```

ACCESS_COARSE_LOCATION is used when we use network location provider for our Android app. But, ACCESS_FINE_LOCATION is providing permission for both providers. INTERNET permission is must for the use of network provider.


For our application to get GPS-information from a device we need to use the class LocationManager and the interface LocationListener.	

## LocationManager:

`locationManager = (LocationManager) getSystemService(LOCATION_SERVICE);`

The Android LocationManager is a class which has access to the location of the device. It has a method called requestLocationUpdates which looks like this:

`requestLocationUpdates(String provider, long minTime, float minDistance, LocationListener listener)`

This method is used to control when we want location updates. We can specify how often we want to get a location update with the minTime parameter. We can also specify the minimum distance (in meters) that the device has to move before we get a new location update with the minDistance parameter. Lastly we also specify which LocationListener we want to attach to our LocationManager. Whenever a new location update is made the attached LocationListeners onLocationChanged method is run.

## LocationListener:

The LocationListener is an interface which implements 4 methods. The methods are:

`abstract void	onLocationChanged(Location location)`

`abstract void	onProviderDisabled(String provider)`

`abstract void	onProviderEnabled(String provider)`

`abstract void	onStatusChanged(String provider, int status, Bundle extras)`

In this example app we use the onLocationChanged and the OnProviderDisabled. 



### OnLocationChanged

As mentioned above whenever location update is sent from the LocationManager the LocationListeners onLocationChanged method is called and a Location is passed. Now we can use the location for whatever we want. In this example we printed the latitude and longitude on two different TextViews. The textView is then updated every time a new location update is made.
In this example we used two different LocationListeners. One which sends a location update 10 times each second, and gets replaced every time the location updates. This is used to see the location change all the time when the device is moved.
The other LocationListener sends a location update only every 10 seconds, and appends the location to the older locations to see a log of previous locations on the screen.

### OnProviderDisabled

The other method used in this app is OnProviderDisabled. This method is as the name tells run whenever the provider, in this case the gps is disabled. In this example we used the method to open a new activity in the settings application where the user can turn on the location service. This activity is opened by using the startActivity method.

`Intent intent = new Intent(Settings.ACTION_LOCATION_SOURCE_SETTINGS);`

`startActivity(intent);`

## Location object
The Location class is a class representing a geographic location.
A location can consist of a latitude, longitude, which represents the coordinates in the geographic coordinate system. It can also consist of other information such as timestamp, bearing, altitude and velocity.

When generating locations with the LocationManager, all locations are guranteed to have a valid latitude, longitude and timestamp, while other parameters are optional. The class has several methods e.g .DistanceBetween() which returns the distance in metres between your object and the given object. 





For developing location aware application in android, it needs location providers. There are two types of location providers:

GPS Location Provider
Network Location Provider

Any one of the above providers is enough to get current location of the user or user’s device. But, it is recommended to use both providers as they both have different advantages. Because, GPS provider will take time to get location at indoor area. And, the Network Location Provider will not get location when the network connectivity is poor.

## Network Location Provider vs GPS Location Provider
Network Location provider is comparatively faster than the GPS provider in providing the location co-ordinates.
GPS provider may be very very slow in in-door locations and will drain the mobile battery.
Network location provider depends on the cell tower and will return our nearest tower location.
GPS location provider, will give our location accurately.


## Steps to get location in Android
Provide permissions in manifest file for receiving location update
Create LocationManager instance as reference to the location service
Request location from LocationManager
Receive location update from LocationListener on change of location

## Provide permissions for receiving location update
To access current location information through location providers, we need to set permissions with android manifest file.

`<manifest ... >`
   
`  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />`
   
`  <uses-permission android:name="android.permission. ACCESS_COARSE_LOCATION" />`
   
`  <uses-permission android:name="android.permission.INTERNET" />`

`</manifest>`

ACCESS_COARSE_LOCATION is used when we use network location provider for our Android app. But, ACCESS_FINE_LOCATION is providing permission for both providers. INTERNET permission is must for the use of network provider.

## Create LocationManager instance as reference to the location service
For any background Android Service, we need to get reference for using it. Similarly, location service reference will be created using getSystemService() method. This reference will be added with the newly created LocationManager instance as follows.

`locationManager = (LocationManager)getSystemService(Context.LOCATION_SERVICE);`

## Request current location from LocationManager
After creating the location service reference, location updates are requested using requestLocationUpdates() method of LocationManager. For this function, we need to send the type of location provider, number of seconds, distance and the LocationListener object over which the location to be updated.
locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 0, 0, this);

## Receive location update from LocationListener on change of location
LocationListener will be notified based on the distance interval specified or the number seconds.
