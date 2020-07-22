# Flickr Map

This script generates a map with markers for all photos in the user's Flickr™ photostream. Click [here](https://hpfilho.github.io/FlickrMap/example/) to see an example.

## Installation

The script was developed to run on _Linux_ systems and need _Python 3.x_ to run. 

To start, open a terminal and execute the following commands:

```
git clone https://github.com/hpfilho/FlickrMap.git
cd FlickrMap
```

The script uses *[Flickr](https://www.flickr.com/)™* and *[Mapbox](https://www.mapbox.com/)™* APIs. To get and use these APIs follow the instructions below.

#### Flickr API key
First, install the [_flickrapi_](https://stuvel.eu/flickrapi) package by typing in a terminal:

```
% pip3 install flickrapi
```
Now, get an API key by visiting the [_Flickr_ API key request page](https://www.flickr.com/services/apps/create/apply/).

After that, create a file __api_credentials.py__ with the following code and with the obtained values:

```python
api_key = u'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
api_secret = u'xxxxxxxxxxxxxxx'
user_id = 'XXXXXXXXXXXX'

```

Then, [authenticate](https://stuvel.eu/flickrapi-doc/3-auth.html#authenticating-without-local-web-server) on _Flickr_ by running:

```
% ./auth2flickr.py
```
A web browser will be opened to get the user approval (in a non-graphical environment, just copy and paste the authorization url in any external web browser). After approve, type in the terminal the generated code.

#### Mapbox API access token

Get an access token by visiting the [Create an access token](https://account.mapbox.com/access-tokens/create) page on [Mapbox](https://www.mapbox.com/) website.

Give a name to the token (e.g.: "Flickr Photos Map") and click on "**Create token**".

Then, type the following command in the terminal:

```
% echo "[YOUR TOKEN]" > mapbox_token
```

## Configuration

By default, the script will generate the map marking only the public photos on the user's photostream, and those with a geolocation set as visible to anyone. 
This can be changed by editing the file 'config.py', and setting the values of the variables _photo_privacy_ and/or _geo_privacy_ as indicated:

```
# Photo Privacy Filter:
# 0 = all photos (public and private)
# 1 = public photos
# 2 = private photos visible to friends
# 3 = private photos visible to family
# 4 = private photos visible to friends & family
# 5 = completely private photos
photo_privacy = 1

# Geolocation Privacy Filter:
# 0 = All
# 1 = Anyone (Recommended)
# 2 = Your contacts
# 3 = Your friends
# 4 = Your family
# 5 = Your friends and family
# 6 = Only you
geo_privacy = 1
```

There is one more option that can be changed, the variable _dont_map_tag_. To exclude a photo from the map, define a tag in this variable and add the same tag to the photo. 
The default tag is _DontMap_:

```
# Photos with this tag
# won't be included on map
dont_map_tag = 'DontMap'
```

There is an additional file needed to run the script: '__header.html__'. This file contains the initial _html_ and _javascript_ code of the map page. 

So, __DO NOT DELETE IT!__

## Usage

Just run the script:

```
% ./generate-map.py
```

The output will be like this:

```
############## Flickr Map ##############
1064 photos will be mapped
Extracting photos coordinates and ids...
Done!
Adding markers...
Done!
533 markers were added
```

The map is generated in the file __'map.html'__, which can be opened in a web browser, such as _Google Chrome_ and _Microsoft Edge_ 
(doesn't work on _Internet Explorer_ and has not been tested on other browsers).
