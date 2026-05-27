**Pyosmium** is a Python library designed for efficiently processing OpenStreetMap (OSM) data, especially when dealing with large files. It works by reading data in a streaming manner, meaning it processes one object (like a node, way, or relation) at a time, without loading the entire file into memory. This makes it great for handling large datasets.

To help explain how this works, imagine the data as a huge book. Instead of reading the entire book all at once (which would take up too much memory), **pyosmium** opens just one page at a time and shows you the content. When you're done with that page, it moves to the next one. This way, it doesn’t need a lot of memory, which is great when the book (or file) is huge.

The downside is that, just like reading a book one page at a time, you can’t jump straight to a specific chapter or section. If you want to access data from a certain part of the file, you have to read through the pages in order, or use techniques like caching to remember parts of the book you’ve already read.

**Pyosmium** can be compared to **generators** in Python, as both handle data efficiently by processing it one piece at a time without loading everything into memory at once.
- **List :  
    A **list** in Python stores all its elements in memory at once. If you have a large dataset (like a list with millions of items), it can quickly consume a lot of memory. If you want to access any item in the list, you can do so directly and instantly. However, with a large list, the downside is that it may not be memory-efficient.
    
- **Generators**:  
    A **generator** in Python is like a lazy iterator that produces one item at a time when you need it, instead of loading everything into memory at once. It’s memory-efficient, just like **pyosmium**. For example, a generator yields each item only when requested, without storing the entire dataset in memory.
    
    This is almost exactly how **pyosmium** works. It reads one object at a time from the data source (like a generator yielding one item), which makes it memory-efficient but also means you can't directly jump to a specific object without processing through others first, much like how a generator works in a sequential manner.


 This is important to always keep in mind. pyosmium never shows you a full data object, it only ever presents a view. That means you can read and process the information about the object but you cannot change it or keep the object around for later. Once you retrieve the next object, the view will no longer be valid.
 
OpenStreetMap data is organised as a topological model. Objects are not described with geometries like most GIS models do. Instead the objects are described in how they relate to points in the world.
An OSM object does not have a pre-defined function. What an object represents is described with a set of properties, the _tags_. This is a simple key-value store of strings.

there are three kinds of objects in OSM: nodes, ways and relations.

#### Nodes
A node is a point on the surface of the earth. Its location is described through its latitude and longitude using projection WSG84.

The main property of a Node is the _location_, a coordinate in WGS84 projection. Latitude and longitude of the node can be accessed either through the `location` property or through the `lat` and `lon` shortcuts
```
for o in osmium.FileProcessor('../data/buildings.opl', osmium.osm.NODE): 
	assert (o.location.lon, o.location.lat) == (o.lon, o.lat)
```

#### Ways
Ways are lines that are created by connecting a sequence of nodes. The nodes are described with the ID of a node in the database. That means that a way object does not directly have coordinates. To find out about the coordinates where the way is located, it is necessary to look up the nodes of the way in the database and get their coordinates.

Representing a way through nodes has another interesting side effect: many of the nodes in OSM are not meaningful in itself. They don't represent a bus stop or lamp post or entrance or any other point of interest. They only exist as supporting points for the ways and don't have any tags.

When a way ends at the same node ID where it starts, then the way may be interpreted as representing an area. If it is really an area or just a linear feature that happens to circle back on itself (for example, a fence around a garden) depends on the tags of the way. 

A Way s essentially an ordered sequence of nodes. This sequence can be accessed through the `nodes` property. An OSM way only stores the ID of each node. This can be rather inconvenient when you want to work with the geometry of the way, because the coordinates of each node need to be looked up

#### Relations
A **relation** in OpenStreetMap (OSM) is essentially an ordered collection of objects, such as nodes, ways, or even other relations. These objects are grouped together within the relation, and each object within the relation can have a specific role. The **role** is a string that describes the function or purpose of the object within that relation. 

However, the important thing to note is that the **OSM data model** doesn't specify exactly how relations should be used or what the members within a relation should represent. The interpretation of a relation and its members is left to the discretion of the user



The topologic nature of the OSM data model means that an OSM object rarely can be regarded in isolation. OSM ways are not meaningful without the location information contained in its nodes. And conversely, changing the location in a way also changes the geometry of the way even though the way itself is not changed. This is an important concept to keep in mind when working with OSM data.

- A **forward reference** means that an object is referenced to by another. Nodes appear in ways. Ways appear in relations. And a node may even have an indirect forward reference to a relation through a way it appear in. Forward references are important when tracking changes. When the location of a node changes, then all its forward references have to be reevaluated.
    
- A **backward reference** goes from an object to its referenced children. Going from a way to its containing nodes means following a backward reference. Backward references are needed to get the complete geometry of an object: given that only nodes contain location information, we have to follow the backward references for ways and relations until we reach the nodes.


Each OSM object type has a corresponding python class:  
**osmium.osm.Relation**
```
for o in osmium.FileProcessor('buildings.opl'): 
	if isinstance(o, osmium.osm.Relation):       
	// if obj.is_relation() 
		print('Found a relation.')
```

#### Reading object tags

Every object has a list of properties, the tags. They can be accessed through the `tags` property, which provides a simple dictionary-like view of the tags. 

```
if obj.tags.get('building') == 'yes':
        print(obj)
        print(obj.tags.get('building'))
```


#### Geometry types

#### Point geometries

OSM nodes are the only kind of OSM object that produce a point geometry. The location of the point is directly stored with the OSM nodes. 

#### Line geometries

Line geometries are usually created from OSM ways. The OSM way object does not contain the coordinates of a line geometry directly. It only contains a list of references to OSM nodes. To create a line geometry from an OSM way, it is necessary to look up the coordinate of each referenced node. pyosmium provides an efficient way to do so: the location storage. The storage automatically records the coordinates of each node that is read from the file and caches them for future use. When later a way is read from a file, the list of nodes in the way is augmented with the appropriate coordinates. Location storage is not enabled by default. To add it to the processing, use the function `with_locations()` of the FileProcessor.

```
for o in osmium.FileProcessor('../data/buildings.opl').with_locations(): 
	if o.is_way(): 
		coords = ", ".join((f"{n.lon} {n.lat}" for n in o.nodes if n.location.valid())) 
		print(f"Way {o.id}: LINESTRING({coords})")
```

#### Areas

OSM defines **areas** in two different ways:
- **Closed Ways**: If a `way` forms a closed loop (first and last node are the same), it can be an area.
- **Relations (Multipolygon/Boundary)**: If an object is tagged as `type=multipolygon` or `type=boundary`, it is explicitly treated as an area.

However, **not all closed ways are areas**—some might just be circular lines (e.g., a fence). The interpretation depends on the **tags**.

Pyosmium introduces a specialized `Area` object, which:
- Handles both ways and relations.
- Assigns a **new ID space** to distinguish between:
    - Areas derived from **ways** (`ID = 2 * way_ID`)
    - Areas derived from **relations** (`ID = 2 * relation_ID + 1`)
- Uses `is_area()` to check if an object is an area.

To enable area processing, you call `.with_areas()` on the `FileProcessor`.

Not every closed way necessarily represents and area. Think of a little garden with a fence around it. If the OSM way represents the garden, then it should be interpreted as an area. If it represents the fence, then it is a line geometry that just happens to go full circle. You need to look at the tags of a way in order to decide if it should become an area or a line, or sometimes even both.

- Areas consist of **outer and inner rings**:
    - `outer_rings()` → Returns exterior boundaries (clockwise).
    - `inner_rings()` → Returns holes inside the polygon (counterclockwise).


- To restrict areas to a bounding box, check:
	- If **any node** in the outer ring is inside the bbox.



----


If you want to process the geometries with Python libraries like [shapely](https://shapely.readthedocs.io/)[1](https://docs.osmcode.org/pyosmium/latest/user_manual/03-Working-with-Geometries/#fn:1) or [GeoPandas](https://geopandas.org/), then the standardized [**geo_interface**](https://gist.github.com/2217756) format can come in handy. pyosmium has a special filter [GeoInterfaceFilter](https://docs.osmcode.org/pyosmium/latest/reference/Filters/#osmium.filter.GeoInterfaceFilter) which enhances pyosmium objects with a `geo_interface` attribute. This allows libraries that support this interface to directly consume the OSM objects. The GeoInterfaceFilter needs location information to create the geometries


#### Filters

Filters can be added to a FileProcessor with the [`with_filter()`](https://docs.osmcode.org/pyosmium/latest/reference/File-Processing/#osmium.FileProcessor.with_filter) function. An arbitrary number of filters can be added to the processor. Simply call the functions as many times as needed. The filters will be executed in the order they have been added.
Filters can have side effects. That means that a filter may add additional attributes to the OSM object it processes and these attributes will be visible for subsequent filters and in the Python processing code. For example, the GeoInterfaceFilter adds a Python `__geo_interface__` attribute to the object.

Filters can be restricted to process only certain types of OSM objects. If an OSM object doesn't have the right type, the filter will be skipped over as if it wasn't defined at all. To restrict the types, call the [`enable_for()`](https://docs.osmcode.org/pyosmium/latest/reference/#osmium.BaseFilter.enable_for) function.

```
fp = osmium.FileProcessor('../data/liechtenstein.osm.pbf')\ .with_filter(osmium.filter.KeyFilter('place').enable_for(osmium.osm.NODE))\ .with_filter(osmium.filter.KeyFilter('boundary').enable_for(osmium.osm.WAY | osmium.osm.RELATION))
```

#### EmptyTagFilter:
This filter removes all objects that have no tags at all. Most of the nodes in an OSM files fall under this category. So even when you don't want to apply any other filters, this one can make a huge difference in processing time

```
print("Total number of tagged objects:", sum(1 for o in osmium.FileProcessor('liechtenstein.osm.pbf') .with_filter(osmium.filter.EmptyTagFilter())))
```

#### EntityFilter :
The Entity filter only lets through objects of the selected type:

```
print("Of which are nodes:", sum(1 for o in osmium.FileProcessor('../data/liechtenstein.osm.pbf') .with_filter(osmium.filter.EntityFilter(osmium.osm.NODE))))
```

On the surface, the filter is very similar to the entity selector that can be passed to the FileProcessor.
However, the two implementations use different mechanism to drop the nodes. When the entity selector in the FileProcessor is used like in the second example, then only the selected entities are read from the file. In our example, the file reader would skip over the ways and relations completely. When the entity filter is used, then the entities are only dropped when they get to the filter. Most importantly, the objects will still be visible to any filters applied _before_ the entity filter.

This can become of some importance when working with geometries. Lets say we can to compute the length of all highways in our file. The location cache needs to see all nodes in order to record their locations. This would not happen if the file reader skips over the nodes. It is therefore imperative to use the entity filter here.

#### KeyFilter
This filter only lets pass objects where its list of tags has any of the keys given in the arguments of the filter.
If you want to ensure that all of the keys are present, use the KeyFilter multiple times:
```
print("Objects with 'building' _or_ 'amenity' key:", 
sum(1 for o in osmium.FileProcessor('../data/liechtenstein.osm.pbf') .with_filter(osmium.filter.KeyFilter('building', 'amenity')))) 

print("Objects with 'building' _and_ 'amenity' key:", sum(1 for o in osmium.FileProcessor('../data/liechtenstein.osm.pbf') .with_filter(osmium.filter.KeyFilter('building')) .with_filter(osmium.filter.KeyFilter('amenity'))))
```

#### TagFilter
This filter works exactly the same as the KeyFilter, only it looks for the presence of whole tags (key and value) in the tag list of the object.



##### Best Option for Large OSM Files :

- **The `osmium.SimpleHandler` or `osmium.FileProcessor` with filters** is the **most efficient** method for processing large OSM files in terms of both **memory and speed**.
	- Designed for handling OSM data incrementally
    - These methods allow you to **stream data** and **filter it on-the-fly**, which means you only store and process what’s necessary.
    - **`osmium.SimpleHandler`** gives you the most control if you need to handle custom tag checks and bounding box filtering.
    - **`osmium.FileProcessor`** provides a higher-level interface with built-in filters, but it might be a bit less flexible if you have very specific processing needs. Both methods are highly efficient for processing large files because they don’t load the entire file into memory at once.

##### When to Use `geopandas`:
- If you need **advanced GIS operations** or you're working with small-to-medium datasets that fit comfortably into memory, `geopandas` can be a great choice.
- It’s useful if you're performing spatial queries, analysis, or want to use a library that integrates well with other data processing tools like `pandas`.
- However, for **large OSM files**, `geopandas` is not as efficient because it requires loading the entire dataset into memory, which can lead to memory issues when dealing with GBs of data.


### Resolution

What is a resolution?? 
the resolution is the pixel size. Like when we say the elevation map has resolution 30 , it means that each pixel represents a 30 meter by 30 meter square on the ground.
So, in other words:
- The elevation value at each pixel tells you the height of the terrain at that spot.
- But it's **not just a point**—it's assumed to be the average elevation over a **30m × 30m area**.

For DEMs, resolution is almost always in **meters** (not pixels or degrees)



### Rasterio
`rasterio` is a powerful Python library to read and write raster geospatial data (like satellite images, elevation models, etc.).


##### Key Concepts 

- **`dataset = rasterio.open(path)`**: 
	- Opens a raster file (e.g., GeoTIFF).
	- `dataset` is an object representing the whole raster.
	- It contains metadata: size, CRS, transform, number of bands, etc.
	- You can query or read data from it.
    
- **`dataset.read(1)`**: 
	- Reads the first raster **band** as a 2D NumPy array (e.g., elevation values).
	- Raster data often has multiple **bands** (like color channels: Red, Green, Blue, or different spectral bands, or elevation data).
    
- **`dataset.index(easting, northing)`**:
	- Converts **map coordinates** to **pixel (row, col)** in the raster grid.
    
- **`band[row, col]`**: 
	- Accesses the raster value at that pixel (e.g., elevation at that location).


##### batch coordinate processing : 

```
dataset.index(e, n)
```
works only for **single coordinates** (`float`, `int`) not a batch of coordinates


for batch processing use 
```
from rasterio.transform import rowcol


transform = dataset.transform
rasterio.transform.rowcol(transform, es, ns)
```
It gives you the **row, col** pixel coordinates for all input coordinates.

```
elevation_vals = band[rows, cols]
```
you can use band with batch of rows, cols and it give values for all rows, cols