---
title: Sample 1 Topic
keywords: sample
summary: "Learn how to pull data from the Arable API"
sidebar: examples_sidebar
permalink: ex1_Downloading.html
simple_map: true
map_name: usermap
box_number: 1
folder: examples
---

# Downloading Data

_Outline_
1. Set credentials in your environment
1. Use credentials to connect to the Arable API
1. Pull info on Devices 
1. Access Device info stored in key:value pairs
1. Explore Device Data and read into dataframe
1. Write Data tables out to a CSV file
1. Access Location info using Device id

## Set credentials in your environment

In [Getting Started](https://pro-soap.cloudvent.net/index.html) we set up our username, password, and tenant in the shell environment. First we need retrieve them here:

  <div class="input_area" markdown="1">

```python
import os
arable_email = os.getenv('ARABLE_EMAIL')
arable_passwd = os.getenv('ARABLE_PASSWD')
arable_tenant = os.getenv('ARABLE_TENANT')

print arable_email, arable_passwd, arable_tenant
```

  </div>
  
{:.output_stream}
  ```
  friendof@arable.com agrofuturism franz_hydro
  ```  

  <div class="input_area" markdown="1">
  
## Use credentials to connect to the Arable API

There are two ways to connect, one is with a username and password, the other is a JSON Web Token ([JWT](https://jwt.io/)) that can be used directly in the header of an HTTP request.

First import the Arable python client you downloaded using `pip install arable`.

</div>

<div class="input_area" markdown="1">

```python
from arable.client import *
```
</div>

We create an instance of the arable client and establish our credentials using the `a.connect()` function.

  <div class="input_area" markdown="1">

```python
a = ArableClient()
if email and password and tenant:
  a.connect(email, password, tenant)

# Get the current time
now = datetime.datetime.now()

# Let's use the last 30 days as a representative sample
start_date = now - datetime.timedelta(days=30)
end_date = now

```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
devices = a.devices()
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
# {k for d in devices for k in d.keys()}
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
#device = devices[0]
for i in range(len(devices)):
    print devices[i]['name'],  devices[i]['last_seen'],  devices[i]['last_post'], devices[i]['last_deploy']
```

  </div>
  
  {:.output_stream}
  ```
  A000780 2018-06-25T17:29:48 2018-06-25T17:29:48 2018-06-23T20:23:34
A000493 2018-06-25T17:29:46.325000 2018-06-25T17:29:46.325000 2018-06-25T17:14:57.459000
A000032 2018-06-25T17:29:48.358000 2018-06-25T17:29:46.229000 2018-06-24T21:25:59.057000
A000061 2018-06-25T17:29:46 2018-06-25T17:29:46 2018-06-25T11:27:35
A000478 2018-06-25T17:29:45.791000 2018-06-25T17:29:45.791000 2018-06-25T16:30:34.098000
A000135 2018-06-25T17:29:45.736000 2018-06-25T17:29:45.736000 2018-06-25T15:39:30.971000
A001086 2018-06-25T17:29:45 2018-06-25T17:29:43 2018-06-25T12:27:53
A000470 2018-06-25T17:29:38 2018-06-25T17:29:38 2018-06-25T05:26:27
A000421 2018-06-25T17:29:32.861000 2018-06-25T17:29:32.861000 2018-06-24T19:25:05.589000
A001002 2018-06-25T17:29:31 2018-06-25T17:29:31 2018-06-19T23:06:30
A000677 2018-06-25T17:29:29.900000 2018-06-25T17:29:27.883000 2018-06-19T20:12:30.173000
B00052 2018-06-25T17:29:26.982000 2018-06-25T17:29:24.678000 2018-06-15T10:52:22.952000
A000152 2018-06-25T17:29:24 2018-06-25T17:29:24 2018-06-24T00:22:03
A000763 2018-06-25T17:29:22.060000 2018-06-25T17:29:19.881000 2018-06-24T02:20:32.606000
A000829 2018-06-25T17:29:12 2018-06-25T17:29:12 2018-06-23T12:21:04
A000934 2018-06-25T17:29:10 2018-06-25T17:29:10 2018-06-23T00:15:30
A001050 2018-06-25T17:29:11.958000 2018-06-25T17:29:09.837000 2018-06-17T16:58:29.212000
A000183 2018-06-25T17:29:07 2018-06-25T17:29:07 2018-06-24T15:24:37
A000955 2018-06-25T17:28:56 2018-06-25T17:28:56 2018-06-24T03:22:15
A000847 2018-06-25T17:28:39 2018-06-25T17:28:39 2018-06-25T09:26:05
A000863 2018-06-25T17:28:36 2018-06-25T17:28:36 2018-06-21T11:10:33
A000590 2018-06-25T17:28:30.803000 2018-06-25T17:28:28.439000 2018-06-13T11:48:36.630000
A000597 2018-06-25T17:28:22 2018-06-25T17:28:22 2018-06-21T19:16:05
A000861 2018-06-25T17:28:04.564000 2018-06-25T17:28:02.392000 2018-06-20T09:12:51.137000

  ```
  

  <div class="input_area" markdown="1">
  
```python
d = a.devices(name=device)
d['name']
```

  </div>
  



  {:.output_data_text}
  ```
  u'A001069'
  ```
  



  <div class="input_area" markdown="1">
  
```python
for i = 
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
print d['name'],  d['last_seen'],  d['last_post'], d['last_deploy']
```

  </div>
  
  {:.output_stream}
  ```
  A001069 2018-06-25T16:09:02 2018-06-25T16:09:02 2018-06-23T01:01:25

  ```
  

  <div class="input_area" markdown="1">
  
```python
sta = d['last_deploy']
end = datetime.now()
end = end.strftime("%Y-%m-%dT%H:%M:%SZ")

df = a.query(select='all', 
               format='csv', 
               devices=[device], 
               measure="raw",
               end=end_date, start=start_date, 
               limit=10000) 

# df = a.query(select='all', 
#                format='csv', 
#                devices=[device], 
#                measure="health", 
#                end=end, start=sta, 
#                limit=1) 

df = StringIO(df)
df = pd.read_csv(df, sep=',', error_bad_lines=False)

# make sure I'm using a datetime object
df['time'] = pd.to_datetime(df['time'])

# # df['RH'] = df['RH']/100.0
# # df['P'] = P
# # df.to_csv('A176_hourly.csv')

# # data.head(2)
# # data.tail(2)
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
df['temp']
```

  </div>
  



  {:.output_data_text}
  ```
  0        NaN
1        NaN
2      17.19
3        NaN
4        NaN
5        NaN
6        NaN
7      17.15
8        NaN
9        NaN
10       NaN
11       NaN
12     17.09
13       NaN
14       NaN
15       NaN
16       NaN
17     17.11
18       NaN
19       NaN
20       NaN
21       NaN
22     17.13
23       NaN
24       NaN
25       NaN
26       NaN
27     17.14
28       NaN
29       NaN
       ...  
863    17.52
864    17.42
865    17.45
866    17.48
867    17.57
868    17.68
869    17.73
870    17.76
871    17.88
872    17.98
873    18.02
874    18.10
875    18.21
876    18.28
877    18.37
878    18.46
879    18.58
880    18.72
881    18.84
882    18.98
883    19.09
884    19.25
885    19.39
886      NaN
887      NaN
888    19.60
889      NaN
890      NaN
891      NaN
892    19.73
Name: temp, Length: 893, dtype: float64
  ```
  



  <div class="input_area" markdown="1">
  
```python
d['signal_strength']
```

  </div>
  



  {:.output_data_text}
  ```
  u'Very Good'
  ```
  



  <div class="input_area" markdown="1">
  
```python
d
```

  </div>
  



  {:.output_data_text}
  ```
  {u'created': u'2018-03-23T16:33:54.619000',
 u'firmware': u'eff57fea-8cd9-4dc7-ac2e-3296e8bfc5e0',
 u'flags': [u'Orientation'],
 u'id': u'58e6ac98b4e1e886de87bb92',
 u'last_deploy': u'2018-06-23T01:01:25',
 u'last_post': u'2018-06-25T16:09:02',
 u'last_seen': u'2018-06-25T16:09:02',
 u'location': {u'id': u'5b23f1aa5d4dc70b312543cb',
  u'name': u'1069 Bob Bendfeldt'},
 u'model': u'4',
 u'name': u'A001069',
 u'org': u'5942be02b4e1e8ced6db2c7e',
 u'owner': u'5b0443f954757d5c77c000e8',
 u'permissions': [u'599c9cc62877ba42397f5462',
  u'5b11ba1df22caa3b450383f3',
  u'5b280baad250685163ca95b4',
  u'5b2983d1f22caa085e6be2ae'],
 u'reported_fw': u'Release-0.2.0.0',
 u'roles': [],
 u'signal_strength': u'Very Good',
 u'state': u'Active',
 u'sync_interval': 4,
 u'updated': u'2018-06-25T16:09:02.247000'}
  ```
  


# Todo
- query language shall be `mark <device>`
- repeat back device
- signal strength in plain language (from devices())
- voltage (from health) 
- GPS (from health or raw)
- T° and RH° (temp and rh from raw) - present in °F
- for all of these get the most recent valid (non-Nan) number
- Synced XX minutes ago
- Deployed on XX date (skip the time)
- you decide how to make it conversational

# Extra Credit
- short url with google map of lat/long
- extract cell id from twilio, get its time zone, return deployed time in local time


  <div class="input_area" markdown="1">
  
```python

```

  </div>
  
