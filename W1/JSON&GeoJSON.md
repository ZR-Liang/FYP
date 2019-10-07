## JSON

------

### JSON

JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is built on two structures: 1) A collection of name/value pairs. It can also be treat as object, record, struct, dictionary,  hash table, keyed list, or associative array. 2) An ordered list of values We can teat it as array, list, or sequence.

------



### Python 

------

Basic Usage:

- json.dump(): It can be used to serialize object as a JSON formatted stream to file. It supports writing to a file.

   

  ```python
  # json.dump(obj, fp, *, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)
  # sort_key: The output of dictionaries will be sorted by key.
  # indent: Json  will be pretty-printed with that indent level.
  
  
  import json
  
  with open('example.json','w') as file:
  		data = {
  			'name1':'value1',
  			'name2':'value2',
  			'name3':'value3',
  		}
  		json.dump(data,file,sort_keys=True, indent=4)
          sile.close()
  ```
  
- json.dumps(): Serialize obj to a JSON formatted str
  ```python
  
  # json.dumps(obj, *, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)
  
  
  import json
  data = {
  	'name1':'value1',
  	'name2':'value2',
  	'name3':'value3',
  }
  json_str = json.dump(data)
  # write data as json to output file 
  with open('output.json', 'w') as file:
      json.dump(data, file)
      file.close()
  ```
  
- json.load(): Deserialize text file or binary file containing a JSON document to a Python object.
  
  ```python
  
  # json.load(fp, *, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)
  with open('example.json', 'r') as file:
          print(json.load(file))
  		file.close()
  ```
  
  
  
- json.loads(): Deserialize a JSON document to a Python object.
  
  ```python
  #json.loads(s, *, encoding=None, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)
  
  with open("example.json", "r") as file:
    print(json.loads(file.read()))
    file.close()
  # It IS WRONG json.loads(file)
  ```
  
  ***Conversion Table:***
  
  | JSON          | Python |
  | :------------ | ------ |
  | object        | dict   |
  | array         | list   |
  | string        | str    |
  | number (int)  | int    |
  | number (real) | float  |
  | true          | True   |
  | false         | False  |
  | null          | None   |
  
  ```python
  # Loop the json get the key value
  # example 1
  dic ={}
  def json_txt(dic_json):
  
  	# if dic_json is not dict then return false 
      if isinstance(dic_json,dict):
      
          for key in dic_json:
          	#if dic_json[key] still is dic
              if isinstance(dic_json[key],dict):
                  print("****key--：%s value--: %s"%(key,dic_json[key]))
                  json_txt(dic_json[key])
                  dic[key] = dic_json[key]
              else:
                  print("****key--：%s value--: %s"%(key,dic_json[key]))
                  dic[key] = dic_json[key]
                  
  # example 2
  data = 
  '''
  {
      "Meta Data": {
          "1. Information": "Daily Prices (open, high, low, close) and Volumes",
          "2. Symbol": "AAPL",
          "3. Last Refreshed": "2017-12-26",
          "4. Output Size": "Compact",
          "5. Time Zone": "US/Eastern"
      },
      "Time Series (Daily)": {
          "2017-12-26": {
              "1. open": "170.8000",
              "2. high": "171.4700",
              "3. low": "169.6790",
              "4. close": "170.5700",
              "5. volume": "33106577"
          },
          "2017-12-22": {
              "1. open": "174.6800",
              "2. high": "175.4240",
              "3. low": "174.5000",
              "4. close": "175.0100",
              "5. volume": "16052615"
          },
          "2017-12-21": {
              "1. open": "174.1700",
              "2. high": "176.0200",
              "3. low": "174.1000",
              "4. close": "175.0100",
              "5. volume": "20356826"
          }
      }
  }
  '''
  data = json.loads(data)
  for key, val in data['Time Series (Daily)'].items():
      print(key, val["1. open"])
  
      
  ## result:
  2017-12-26 170.8000
  2017-12-22 174.6800
  2017-12-21 174.1700
  ```
  
  
  
  
  
  ## GeoJSON
  
  ------
  
  ### GeoJSON:
  
  It is a special JSON used to present geopolitical data.
  
  ```python
  # WE PUT ALL INFORMATION INTO features
  {
  	"type": "FeatureCollection",
  	"features":[]
  }
  
  
  # Example
  {
         "type": "FeatureCollection",
         "features": [{
             "type": "Feature",
             "geometry": {
                 "type": "Point",
                 "coordinates": [102.0, 0.5]
             },
             "properties": {
                 "prop0": "value0"
             }
         }, {
             "type": "Feature",
             "geometry": {
                 "type": "Polygon",
                 "coordinates": [
                     [
                         [100.0, 0.0],
                         [101.0, 0.0],
                         [101.0, 1.0],
                         [100.0, 1.0],
                         [100.0, 0.0]
                     ]
                 ]
             },
             "properties": {
                 "prop0": "value0",
                 "prop1": {
                     "this": "that"
                 }
             }
         }]
     }
  
  
  # Geometry Object: feature point
  	{
      	"type": "Point", 
      	"coordinates": [30, 10]
  	}
  
      
  # Geometry Object: point
  	{
          "type":"MultiPoint",
          "coordinates":[
              	[105.380859375,31.57853542647338],
                  [105.580859375,31.52853542647338]
              ]
  	}
      
      
  # Geometry Object: MultiPoint
  	{
          "type":"MultiPoint",
          "coordinates":[
              	[105.380859375,31.57853542647338],
                  [105.580859375,31.52853542647338]
              ]
  	}
  	
      
  # Geometry Object: LineString
  	{
          "type":"MultiPoint",
          "coordinates":[
              	[105.380859375,31.57853542647338],
                  [105.580859375,31.52853542647338]
              ]
  	}
      
      
  # Geometry Object: MultiLineString
  	{ 
          "type": "MultiLineString",
      	"coordinates": [
          	[ [100.0, 0.0], [101.0, 1.0] ],
          	[ [102.0, 2.0], [103.0, 3.0] ]
        ]
  	}
      
      
  # Geometry Object: Polygon
  	{
          "type":"Polygon",
          "coordinates":[
          	[
              	[106.10595703125,33.33970700424026],
                  [106.32568359375,32.41706632846282],
                  [108.03955078125,32.2313896627376],
                  [108.25927734375,33.15594830078649],
                  [106.10595703125,33.33970700424026]
              ]
          ]
  	}
      
      
      
  # Geometry Object: MultiPolygon
  	# type 1 without intersect
      {
    		"type": "MultiPolygon",
    		"coordinates":
      	[ 
              #Polygon 1
          	[
              	[
                 		[109.2041015625,30.088107753367257],
                 		[115.02685546875,30.088107753367257],
                  	[115.02685546875,32.7872745269555],
                  	[109.2041015625,32.7872745269555],
                  	[109.2041015625,30.088107753367257]
              	]
          	],
              #Polygon 2
          	[
              	[
                  	[112.9833984375,26.82407078047018],
                  	[116.69677734375,26.82407078047018],
                  	[116.69677734375,29.036960648558267],
                  	[112.9833984375,29.036960648558267],
                  	[112.9833984375,26.82407078047018]
              	]
          	]
      	]
     }
      # type 2 nesting the small one at first
      {
    		"type": "MultiPolygon",
    		"coordinates":
      	[ 
              #Polygon 1 (small size)
          	[
              	[
                 		 [101.6455078125,27.68352808378776],
                      [114.78515624999999,27.68352808378776],
                      [114.78515624999999,35.209721645221386],
                      [101.6455078125,35.209721645221386],
                      [101.6455078125,27.68352808378776]
              	]
          	],
              #Polygon 2 (larger size)
          	[
              	[
                  	[104.2822265625,30.107117887092357],
                      [108.896484375,30.107117887092357],
                      [108.896484375,33.76088200086917],
                      [104.2822265625,33.76088200086917],
                      [104.2822265625,30.107117887092357]
              	]
          	]
      	]
     }
      '''
      [
          [
              [
              	coordinates
          	]
          ],
          [
              [
                  coordinates
              ]
          ]
      ]
      '''
      
      #type 3 MultiPolygon with hole
      {
          "type": "MultiPolygon",
          "coordinates":
      	[ 
          	[
             		[
                      # hole
                  	[101.6455078125,27.68352808378776],
                  	[114.78515624999999,27.68352808378776],
                  	[114.78515624999999,35.209721645221386],
                  	[101.6455078125,35.209721645221386],
                  	[101.6455078125,27.68352808378776]
                  
            
              	],
              	[
                  [104.2822265625,30.107117887092357],
                  [108.896484375,30.107117887092357],
                  [108.896484375,33.76088200086917],
                  [104.2822265625,33.76088200086917],
                  [104.2822265625,30.107117887092357]
              	]
          	]
      	]
      }
      '''
      [
          [
              [
                  coordinates
              ],
              [
                  coordinates
              ]
          ]
      ]
      '''
      
      
  # Geometry Object: GeometryCollection
  {
      "type": "GeometryCollection",
      "geometries": [
          {
           "type": "Point",
            "coordinates": [108.62, 31.02819]
           }, {
           "type": "LineString",
            "coordinates": [[108.896484375,30.1071178870],
            [108.2184375,30.91717870],
            [109.5184375,31.2175780]]
           }]
  }
  '''It doesn't need write into FEatureClooection'''
  
  ```
  
  
  
  
