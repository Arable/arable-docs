---
title: Downloading Data
keywords: coding
summary: "Learn how to pull data from the Arable API"
sidebar: examples_sidebar
permalink: ex1_Downloading.html
simple_map: true
map_name: usermap
box_number: 1
folder: examples
---

## Introduction

A REST API is somewhat universal - - you can access it from Mac, Windows, and Linux machines, using python, bash, java, js, or many other languages.  Here, we will focus on the OS we use in-house (OS X), the language we us in our production environment (python), and our preferred prototyping tool ([jupyter](http://www.jupyter.org/)).  

If you are working in other systems and languages, let us know! We'd love to highlight your work here.

This example will mostly be about basic python and jupyter.  Example 2 will mostly be related to using Pandas, a python framework used widely data science.  Example 3 will mostly be related to Matplotlib, a framework for visualization.  Example 4 will mostly be related to using numpy, a framework for doing calculations in python.

If you haven't done so already, fire up jupyter using the `ipy` command we added to your bash environment, or with `jupyter notebook` if you haven't.

## Set credentials in your environment

In [Getting Started](https://pro-soap.cloudvent.net/index.html) we set up our username, password, and tenant in the shell environment. First we need retrieve them here:

```python
import os
arable_email = os.getenv('ARABLE_EMAIL')
arable_passwd = os.getenv('ARABLE_PASSWD')
arable_tenant = os.getenv('ARABLE_TENANT')

print arable_email, arable_passwd, arable_tenant
```
  
{:.output_stream}
```
friendof@arable.com agrofuturism franz_hydro
```  
  
## Use credentials to connect to the Arable API

There are two ways to connect, one is with a username and password, the other is a JSON Web Token ([JWT](https://jwt.io/)) that can be used directly in the header of an HTTP request.

First import the Arable python client you downloaded using `pip install arable`.

```python
from arable.client import *
```

Next use the ArableClient to make a connection with your credentials:


```python
a = ArableClient()
a.connect(arable_email, arable_passwd, arable_tenant)
```

You can get your bearer token directly from the header of the response:


```python
auth_token = a.header['Authorization']
print auth_token
```
  
{:.output_stream}
```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJodHRwOi8vYXBpLmFyYWJsZS5jb20iLCJpYXQiOjE1MzE4MzgyODQsImp0aSI6IjVlNzIyYjU4NDY2ZDQ4N2Y4OGI5ODVkMTM0OTk5MjAyIiwiYXVkIjoiYXBpLmFyYWJsZS5jb20iLCJzY29wZSI6ImM2YjllMTIxLTFiZjItNDNkMS1hNDYwLTI3NWIxZWI0ODdhOSJ9.n3K8bES7-Wko5urpwBO24w2JZQrHoABtL1b_ssymtHs
```

For the time being, we're not going to use the token method, we're just going to use ArableClient.

## Pull info on Devices

Use `a.devices()` to retrieve metadata about the devices you have permissions on.

{% include note.html content="Note, this returns a max of 24 devices.  We don't yet support pagination." %}


```python
devices = a.devices()
```

Let's list out the dictionary for a device:

```python
list(devices[0])
```

{:.output_stream}
```
[u'sync_interval',
 u'updated',
 u'name',
 u'roles',
 u'created',
 u'last_deploy',
 u'firmware',
 u'state',
 u'reported_fw',
 u'signal_strength',
 u'flags',
 u'location',
 u'owner',
 u'org',
 u'model',
 u'permissions',
 u'last_post',
 u'id',
 u'last_seen']
```

Let's look at one device in detail to understand what is the data that gets stored. 

For an in-depth reference on what all these mean, make sure to check out the [API Documentation](https://pro-soap.cloudvent.net/API_landing_page.html)

```python
device = 'A000176'

d = a.devices(name=device)

d
```

{:.output_stream}
```
{u'created': u'2017-12-13T18:01:37.061000',
 u'firmware': u'eff57fea-8cd9-4dc7-ac2e-3296e8bfc5e0',
 u'flags': [u'GPS', u'Orientation'],
 u'id': u'58e65d68b4e1e886020c517e',
 u'last_deploy': u'2018-07-16T05:28:34',
 u'last_post': u'2018-07-17T14:33:41',
 u'last_seen': u'2018-07-17T14:33:41',
 u'location': {u'id': u'5b043a2f17edbb00015afa42',
  u'name': u'UNLTAPS 2, 60% Irr.'},
 u'model': u'4',
 u'name': u'A000176',
 u'org': u'593b753217d33383c09bb435',
 u'owner': u'593b75b417d33383c09bb436',
 u'permissions': [u'5b298296d250685163ca9a58',
  u'5b298296d250685163ca9a57',
  u'5b4ce79b720b5915ea099a43',
  u'5b0dbb9254757d66aebe5cca',
  u'5b2040fff22caa2951fad998',
  u'5b31130c720b596b63118713',
  u'5b2d62e9720b596b631180a2'],
 u'reported_fw': u'Release-0.2.0.0',
 u'roles': [],
 u'signal_strength': u'Very Good',
 u'state': u'Active',
 u'sync_interval': 4,
 u'updated': u'2018-07-17T14:33:42.013000'}
 ```

Note you can also access this device directly using its serial number or its unique id.  

It may seem like a headache to use such a long and unwieldy identifier, but it is through this unique ID that devices are mapped to locations, users, and organization.

```python
device_id = d['id']

d = a.devices(device_id)

device_id
```
{:.output_stream}
```
u'58e65d68b4e1e886020c517e'
```

## Access Device info stored as key:value pairs

Because Device info is stored in JSON, it is easy to extract info out of it using `['key']` syntax:

```python
devices = a.devices()
for i in range(len(devices)):
    print devices[i]['name'], devices[i]['signal_strength']
```

{:.output_stream}
```
A000176 Very Good
A000654 Good
A000149 Very Good
A000136 Very Good
A000069 Very Good
A000172 Very Good
A000153 Very Good
A000148 Very Good
A000152 Very Good
A000100 Very Good
A000652 Weak
A000651 Good
A000655 Very Good
A000183 Very Good
A000653 Weak
A000177 Very Good
```

## Explore Device Data

The real action is of course exploring the data that comes from the Mark.

The data comes in a number of separate tables, which are explained in detail in the [API Documentation](https://pro-soap.cloudvent.net/API_landing_page.html)

* hourly
* daily
* health
* aux_raw

The data can be pulled using the Arable python client's `a.query()` function, with parameters that govern which device, which time period, and which table.

```python
from io import StringIO
import pandas as pd

device = 'A000176' 

sta = "2018-07-04 08:00:00"
end = "2018-07-07 08:00:00"

hourly = a.query(select='all', 
             format='csv', 
             devices=[device], 
             measure='hourly', 
             order='time', 
             end=end, start=sta) 

hourly = StringIO(hourly)
hourly = pd.read_csv(hourly, sep=',', error_bad_lines=False)
```

Note that we read the data into a [pandas](https://pandas.pydata.org/) dataframe.  We do almost all of our analysis in Pandas.

Let's list the data we get from `hourly`:

```python
list(hourly)
```

{:.output_stream}
```
['time',
 'device',
 'location',
 'lat',
 'long',
 'B1dw',
 'B1uw',
 'B2dw',
 'B2uw',
 'B3dw',
 'B3uw',
 'B4dw',
 'B4uw',
 'B5dw',
 'B5uw',
 'B6dw',
 'B6uw',
 'B7dw',
 'B7uw',
 'LWdw',
 'LWuw',
 'LfW',
 'P',
 'SLP',
 'PARdw',
 'PARuw',
 'RH',
 'SWdw',
 'SWuw',
 'Tabove',
 'Tair',
 'Tbelow',
 'Tdew',
 'prate',
 'precip']
```

```python
daily = a.query(select='all', 
             format='csv', 
             devices=[device], 
             measure='daily', 
             order='time', 
             end=end, start=sta) 

daily = StringIO(daily)
daily = pd.read_csv(daily, sep=',', error_bad_lines=False)
list(daily)
```

{:.output_stream}
```
['time',
 'device',
 'location',
 'lat',
 'long',
 'CGDD',
 'Cl',
 'ET',
 'GDD',
 'LfAirDelta',
 'NDVI',
 'SWdw',
 'maxT',
 'meanT',
 'minT',
 'prate',
 'precip',
 'SLP',
 'Kc',
 'ETc']
```

And so on for `health`:

{:.output_stream}
```
['time',
 'device',
 'lat',
 'long',
 'batt_current',
 'batt_pct',
 'batt_volt',
 'err0',
 'err1',
 'err2',
 'err3',
 'err4',
 'orient_x',
 'orient_y',
 'orient_z',
 'elev',
 'sys_temp',
 'pres_temp',
 'thcouple_volt',
 't_conn',
 't_sync',
 'msg_bytes',
 'tot_bytes',
 'tz',
 'fw',
 'reset',
 'rssi',
 'burn_in',
 'auxb_present',
 'auxb_charging',
 'auxb_rev',
 'iccid']
 ```

When we ask for `aux_raw` we'll get an error because this device has no aux plugged in.  

```python
aux_raw = a.query(select='all', 
             format='csv', 
             devices=[device], 
             measure='aux_raw', 
             order='time', 
             end=end, start=sta) 

aux_raw = StringIO(aux_raw)
aux_raw = pd.read_csv(aux_raw, sep=',', error_bad_lines=False)
list(aux_raw)
```

{:.output_stream}
```bash
EmptyDataError: No columns to parse from file
```

This "No columns to parse" error is useful to recognize.  When you get it, try changing the parameters of the request, especially the start and end times, to make sure the request will collect valid data.

## Write dataframes out to a CSV file

This one is easy in pandas:

```python
hourly.to_csv('A000176.csv')
```

## Access Location info using Device id

We found some useful measures anout the Device using the Device id, now it's time to use that Device ID to access the location associated with it.  Here we'll find this like its latitude, longitude, height above sea level and the like.

To do this we'll need to access the API directly, without use of the Arable python client.

Recall that you can get your bearer token from the header of the initial response, and that we can get the current location_id from the device structure.

```python
auth_token = a.header['Authorization']

location_id = a.devices(name='A000176')['location']['id']
```

Next let's compose an HTTP `GET` request to the Arable API, along with our credentials, to get the Location info.

```python
import requests

base = 'https://api-user.arable.cloud/api/v1/'
path = '/locations/'
url = base + path + location_id

response = requests.get(url, headers = {'Authorization': auth_token})
location = response.json()

location
```

{:.output_stream}
```
{u'addr_city': u'North Platte',
 u'addr_postcode': u'69101',
 u'addr_state': u'NE',
 u'county': u'Lincoln County',
 u'created': u'2018-05-22T15:41:35.489000',
 u'current_device': {u'created': u'2017-12-13 18:01:37.061000',
  u'firmware': u'eff57fea-8cd9-4dc7-ac2e-3296e8bfc5e0',
  u'id': u'58e65d68b4e1e886020c517e',
  u'last_deploy': u'2018-07-16 05:28:34',
  u'last_post': u'2018-07-17 16:33:54',
  u'last_seen': u'2018-07-17 16:33:54',
  u'model': u'4',
  u'name': u'A000176',
  u'org': u'593b753217d33383c09bb435',
  u'owner': u'593b75b417d33383c09bb436',
  u'permissions': u"[ObjectId('5b298296d250685163ca9a58'), ObjectId('5b298296d250685163ca9a57'), ObjectId('5b4ce79b720b5915ea099a43'), ObjectId('5b0dbb9254757d66aebe5cca'), ObjectId('5b2040fff22caa2951fad998'), ObjectId('5b31130c720b596b63118713'), ObjectId('5b2d62e9720b596b631180a2')]",
  u'reported_fw': u'Release-0.2.0.0',
  u'roles': u'[]',
  u'state': u'Active',
  u'sync_interval': u'4',
  u'updated': u'2018-07-17 16:33:54.751000'},
 u'elevation': 862.0997924804688,
 u'gps': {u'coordinates': [-100.77352, 41.08763], u'type': u'Point'},
 u'id': u'5b043a2f17edbb00015afa42',
 u'last_updated': u'2018-05-22T15:41:35',
 u'name': u'UNLTAPS 2, 60% Irr.',
 u'notes': u'',
 u'org': u'593b753217d33383c09bb435',
 u'permissions': [u'5b298296d250685163ca9a58',
  u'5b298296d250685163ca9a57',
  u'5b4ce79b720b5915ea099a43',
  u'5b0dbb9254757d66aebe5cca',
  u'5b2040fff22caa2951fad998',
  u'5b31130c720b596b63118713',
  u'5b2d62e9720b596b631180a2'],
 u'radius': 1.0,
 u'start_date': u'2018-05-22T15:41:35',
 u'state': u'Confirmed',
 u'tags': [],
 u'time_offset': -18000}
```

You can see that the location is device agnostic - - it has the device information stored as `current_device` but this location could just as easily have a different device swapped in or out.

As well, there are location-specific values that don't depend on the device, including the lat/long, elevation, and time offset (to convert UTC to local time).

{% include note.html content="Note, there is a strong likelihood that the Locations structure will continue to evolve, which is why it is not included in the ArableClient." %}

```python
print location['current_device']['name'], location['gps']['coordinates'], location['time_offset']
```
  
{:.output_stream}
```
A000176 [-100.77352, 41.08763] -18000
```

We won't get to functions until the 4th tutorial, but if you want, you can wrap this up handle exceptions and make it easy to use.

```python
def location_info(loc_id, auth_token):
    '''
    Queries location api for metadata
    : param loc_id: alphanumeric location id; 24 character string
    : param auth_token: authorization credentials
    : return: location metadata
    '''

    #base = 'https://api.arable.com/dev3'
    base = 'https://api-user.arable.cloud/api/v1/'
    path = '/locations/'
    url = base + path + loc_id
    headers = 'Bearer ' + auth_token

    try:
        response = requests.get(url, headers = {'Authorization': headers})
        response = response.json()
    except Exception:
        print('Unable to get location data with url {}'.format(url))
        exit(1)  
    return response
```

Great job! Now head over to the [Data Wrangling](https://pro-soap.cloudvent.net/ex1_Wrangling.html) tutorial! 

Questions, comments, corrections?  Write the author: adam@arable.com




