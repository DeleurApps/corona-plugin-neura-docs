# Functions


## **addDevice()**

### Overview

Opening a device picker screen.
**Note**:*User must be logged in for this method.*

### Syntax

    neura.addDevice(options, listener)

#### options (optional)
_[Table](https://docs.coronalabs.com/api/type/Table.html)._ A table of options. If none are provided, the default device picker screen is shown. Parameters:

##### *deviceName* (optional)
_[String](https://docs.coronalabs.com/api/type/String.html)._ We'll search the deviceName in our devices list, and add it automatically. Adding a device without displaying our device picker screen. 

- Note that authorization WebView required for connecting the device might still be shown. 
- Note that deviceName isn't case sensitive, meaning if you pass device_name and the device's name is actually Device_naME, then it's still valid, and will be added. 
 
You can get all the devices (and their names) by calling [neura.getKnownDevices()](#getKnownDevices) 

##### *deviceCapabilityNames* (optional)
_[Table](https://docs.coronalabs.com/api/type/Table.html)._ Opening a device picker screen with devices has at least one capability from the deviceCapabilities list provided. We'll only show devices which your user hasn't added yet.

For example, if deviceCapabilities = {"sleepQuality", "heartRateMeasurement"} we'll present devices which are either sleepQuality or scale_measure (if a device is sleepQuality and heartRateMeasurement we'll present it as well). 

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **addPlace()**

### Overview

TODO


## **authenticate()**

### Overview

Authenticating your user with Neura : login or sign up a new user.

### Syntax

    neura.authenticate(listener)

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **connect()**

### Overview

Connecting to neura and firebase. Check [Introduction](index.md) for more info.

### Syntax

    neura.conenct(options, listener)

#### options (required)
_[Table](https://docs.coronalabs.com/api/type/Table.html)._ A table of options. Parameters:

##### *appUid* (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ Neura App UID.

##### *appSecret* (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ Neura App Secret.

##### *firebase* (optional)
_[Table](https://docs.coronalabs.com/api/type/Table.html)._ Table of Firebase parameters to receive push notifications. Should include `apiKey`, `applicationId`, and `gcmSenderId` keys.

#### listener (required)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ General listener for all events if none is provided in the function call.


## **disconnect()**

### Overview

Disconnecting NeuraApiClient instance.

### Syntax

    neura.disconnect()



## **enableAutomaticallySyncLogs()**

### Overview

A log file will be sent to our servers, in order to track issues your user might be having. 
**By default** Syncing logs is disabled.

### Syntax

    neura.enableAutomaticallySyncLogs(enable)

#### enable (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ sending automatically logs to our server, false otherwise.


## **enableNeuraHandingStateAlertMessages()**

### Overview

Neura uses multiply sensors and permission, we're tracking when :
- (On Marshmallow os and above) A permission isn't granted by your user, and is required by Neura to work. **Fyi** this applies only for permissions that are critical, fe - location. 
- Sensors are disabled by the user(location/wifi/bluetooth/network). **Fyi** This only means that the sensors are disabled, not when there's no wifi available fe. 

**We'll alert for the disabled sensors whenever Neura sdk might need it.** 

**By default Neura alert on sensors and permission is enabled.**

If you choose to enable this feature, and let us handle a connection with your user, the flow is described below : 

1. Neura detects that a sensor is disabled or permission is missing and is needed at the moment. 
2. A notification for the user will be presented. 
3. If the user presses this notification:

3a. When permission missing: A transparent activity is opened, with the standard permission dialog. If user selects "Never ask again", we won't display the notification anymore.

3b. When sensor is disabled: An intent for opening the sensors's settings will be called.

### Syntax

    neura.enableNeuraHandingStateAlertMessages(enable)

#### enable (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ true if you want neura to handle alerting the user on permission missing or sensors disabled, false otherwise(by default enable = true : Neura will communicate with your user when a permission is missing).


## **forgetMe()**

### Overview

Calling forgetMe method will disconnect your Neura account, revoke all permissions and stop any notificatiogns between Neura and your application. 
Examples : 

1. forgetMe(false, listener) will do a 'silence' disconnection from neura. 
2. forgetMe(true, listener) will display an 'are you sure' dialog, followed by disconnection from neura if the user presses 'yes'. 

**Note:** *User must be logged in for this method.*

### Syntax

    neura.forgetMe(showAreYouSureDialog, listener)

#### showAreYouSureDialog (optional)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ true if you want an "are you sure" dialog to be displayed to your user, false otherwise("silent" forget me). **Default**: `false`

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getAppPermissions()**

### Overview

Receiving the permissions an application has as declared on the [developer's console.](https://dev.theneura.com/console/apps)

### Syntax

    neura.getAppPermissions(listener)

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getDailySummary()**

### Overview

Returns a user's wellness information for a single day. Daily summary is calculated from the time when the user woke on the requested date until the time the user woke on the following calendar day (date + 1 day). If Neura is unable to identify when the user woke, then daily summary is unavailable for that day.

To retrieve daily data, permission for dailySummary is required. 
For more information, go to [here](https://dev.theneura.com/docs/api/insights#sleep). **Note:** *User must be logged in for this method.*

### Syntax

    neura.getDailySummary(timestamp, listener)

#### timestamp (required)
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ Timestamp of the day to calculate daily summary. Can be any timestamp within the day.

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getKnownCapabilities()**

### Overview

Fetching all the known capabilities for devices. 

**Returns**: a table of json objects for every capability.

**Note:** *User must be logged in for this method.*

### Syntax

    local capabilities = neura.getKnownCapabilities()


## **getKnownDevices()**

### Overview

Fetching all the known devices Neura has to offer. 
**Note:** *User must be logged in for this method.*

### Syntax

    neura.getKnownDevices(listener)

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getLocationBasedEvents()**

### Overview

**Returns**: a table of events which are location based events. 

- fe : userArrivedHome - where home is a location. 
- fe : userArrivedToActiveZone - where ActiveZone represents a location. 
- fe : userStartedWalking - This event is NOT a location based event, and won't be in the list. 
**Note:** *User must be logged in for this method.*

### Syntax

    local locationBasedEvents = neura.getLocationBasedEvents()


## **getMissingDataForEvent()**

### Overview

Opening missing data flow screen. Lets examine [neura events](https://dev.theneura.com/docs/api/events) : There are plenty of 'personal places' events related. Neura allows your user to add multiply places for most of the places on the list except for home. 
If the event isn't related to home - this method will always open a picker for your user. 

fe : eventName = 'userArrivedAtAirport' - since there are plenty of airports, even if you set up an airport, you can still add more airports. 

Note that there might be several labels that's missing for each event, so, listener will be called several times, each time for a missing label. 
A boolean for success/fail will be returned in listener 

**Note:** *User must be logged in for this method.*

### Syntax

    neura.getMissingDataForEvent(eventName, listener)

#### eventName (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ event to check if all the require fields exists.

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getPermissionStatus()**

### Overview

TODO


## **getSdkVersion()**

### Overview

**Returns:** SDK Version string

### Syntax

    local sdkVersion = neura.getSdkVersion()


## **getSleepProfile()**

### Overview

Returns a user's sleep information during a period of time beginning on startTimestamp and ending on endTimestamp, inclusive. 
Please note that the lightSleep, deepSleep, and efficiency metrics are only available when the user is connected to an activity tracker.

To retrieve sleep data, permission for sleepData is required. 
For more information, go to [here](https://dev.theneura.com/docs/api/insights#sleep). **Note:** *User must be logged in for this method.*

### Syntax

    neura.getSleepProfile(startTimestamp, endTimestamp, listener)

#### startTimestamp (required)
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ start time for calculating sleep profile.

#### endTimestamp (required)
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ start time for calculating sleep profile.

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getSubscriptions()**

### Overview

Receiving all the subscriptions a user has to an application. 
**Note:** *User must be logged in for this method.*

### Syntax

    neura.getSubscriptions(listener)

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getUserDetails()**

### Overview

Receiving user's details. 
**Note:** *User must be logged in for this method.*

### Syntax

    neura.getUserDetails(listener)

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getUserPhone()**

### Overview

Receiving user's phone as authenticated with Neura api([neura.authenticate()](#authenticate)) 
**Note:** *User must be logged in for this method.*

### Syntax

    neura.getUserPhone(listener)

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **getUserPlaceByLabelType()**

### Overview

The user's place related address. For example, if the placeName is home, we'll return the home address. 
There could be multiply locations for each placeName, so we're returning a list of PlaceNode. 

You can view the full list of events here, for each event, you can extract its placeName. For example, for the event : userLeftSchoolCampus, the placeName is : SchoolCampus(case sensitive isn't mandatory). 
**Note:** *User must be logged in for this method.*

**Returns:** Table of json objects for places.

### Syntax

    local places = neura.getUserPlaceByLabelType(placeName)

#### placeName (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ home, work, gym, etc... 
Check out the full list of [available labels](https://dev.theneura.com/docs/api/labels).


## **getUserSituation()**

### Overview

Returning the user's whereabouts (locations & activities) for specific timestamp. 
**Note:** *User must be logged in for this method.*

### Syntax

    neura.getUserSituation(timestamp, listener)

#### timestamp (required)
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ Receiving the user's status and whereabouts before timestamp, during timestamp and after timestamp.

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **hasDeviceWithCapability()**

### Overview

**Note:** *User must be logged in for this method.*

**Returns:** true if user has a device with the capabilityName, false otherwise.

### Syntax

    local hasDevice = neura.hasDeviceWithCapability(capabilityName)

#### capabilityName (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ capability name as can be fetched from [neura.getKnownCapabilities()](#getKnownCapabilities)


## **isLoggedIn()**

### Overview

Check if user is logged in to Neura.

**Returns:** true if the user is logged in to Neura. If user is logged in, you may call any api method in this class, if user isn't logged in, please call [neura.authenticate()](#authenticate).

### Syntax

    local isLoggedIn = neura.isLoggedIn()


## **isMissingDataForEvent()**

### Overview

Returning whether the event missing required fields in order for the sdk to detect when it occurs. 

- fe : eventName = 'userArrivedToGym' - return true if gym exists, false otherwise. 
- fe : eventName = 'userArrivedWorkFromHome' - return true if work or home(or both) doesn't exist. 
- fe : eventName = 'userArrivedAtPharmacy' - return true if your user has at least 1 pharmacy in his places. 

Plus, if both home and work exists to the user, we'll consider this event as complete, there's no need to set any more data in order for the sdk to detect the event. 
**Note:** *User must be logged in for this method.*

### Syntax

    local isMissingData = neura.isMissingDataForEvent(eventName)

#### eventName (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ event to check if all the require fields exists.


## **registerFirebaseToken()**

### Overview

If you've decided to [neura.subscribeToEvent()](#subscribeToEvent) with push, you need to use [neura.registerFirebaseToken()](#registerFirebaseToken) at least once in order to register your user with push. 
Please follow our [Neura Push integration guide](https://dev.theneura.com/docs/guide/android/pushnotification). 

We recommend calling this method when callback from calling [neura.authenticate()](#authenticate) is received.

### Syntax

    neura.registerFirebaseToken()


## **removeSubscription()**

### Overview

Removing subscription to a specified event. 
Neura handles retry policy, and will try to delete subscription 3 times at the most. 
Note that this call is similar to [neura.subscribeToEvent()](subscribeToEvent).
**Note:** *User must be logged in for this method.*

### Syntax

    neura.removeSubscription(eventName, eventIdentifier, listener)

#### eventName (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ Subscription to be removed from this event.

#### eventIdentifier (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ The event identifier will be part of the data sent to your webhook when Neura identifies an event for this subscription. It's there for you to attach a user identification, for example. The webhook identifier is the one you gave while registering the app.

#### listener (optional)
_[Listener](https://docs.coronalabs.com/api/type/Listener.html)._ Callback to receive results. Event is sent to the default listener provided in [neura.connect()](#connect) if no listener is provided.


## **sendFeedbackOnEvent()**

### Overview

Sending Neura a feedback for an event received. 
**Note:** *User must be logged in for this method.*

### Syntax

    neura.sendFeedbackOnEvent(neuraId, approved)

#### neuraId (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ neuraID received on your listener which catches the event by fcm or webhook.

#### approved (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ true if user approved that the event occurred, false otherwise.


## **shouldSubscribeToEvent()**

### Overview

**Returns:** true if [neura.subscribeToEvent()](#subscribeToEvent) should be called to eventName, false when the eventName is not valid, or, the eventName is a service (for example : dailyActivitySummary) and in this case - there's no need to subscribe to services, you can request services without subscribing, as long as they're declared on the permissions of your application. 
**Note:** *User must be logged in for this method.*

### Syntax

    local shouldSubscribe = neura.shouldSubscribeToEvent(eventName)

#### eventName (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ As taken from events listed on Neura dev site.


## **simulateAnEvent()**

### Overview

Simulating generating an event 
**Note:** *User must be logged in for this method.*

### Syntax

    neura.simulateAnEvent()


## **subscribeToEvent()**

### Overview

Adding subscription for a specified event. 
Neura handles retry policy, and will try to subscribe 3 times at the most. 
Note that this call is similar to [neura.removeSubscription()](#removeSubscription).
**Note:** *User must be logged in for this method.*

### Syntax

    neura.subscribeToEvent(eventName, eventIdentifier, listener)

#### eventName (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ Subscription to be added to this event.

#### eventIdentifier (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ The event identifier will be part of the data sent to your webhook when Neura identifies an event for this subscription. It's there for you to attach a user identification, for example. The webhook identifier is the one you gave while registering the app.