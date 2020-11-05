# Homework - Binary Data, Formats, and Viz


Homework for module on binary data and formats.


##  Problem 1

Suppose you are programming a UAV for which the flight path is defined by a user-provided sequence of coordinates ($x$, $y$, and $z$) with summary information stored at a UTF-8 string.  The UAV is powered by a simple microcontroller that requires a single binary file be loaded.  This file format is defined as follows:

```
bytes               type              description
-------------------------------------------------------------
0x000000-0x000003:  4-byte int        M = number of characters
0x000004-0x000008:  4-byte int        N = number of coordinates                                    
0x000009-0x??????:  string (utf-8)    flight path info as M bytes
0x??????-0x??????:  8-byte float      coordinates arranged as
                                      x0,y0,z0,x1,y1,...,zN
-------------------------------------------------------------
```

All values are little endian.

Write a Python function `encode(coords, s='flight_path.b')`
that produces the file and a corresponding function
`decode(s)` that returns `coords`.  Here, `coords` is a
list of coordinate tuples of the form `(longitude, latitude, altitude)`.

Here is some data you could use for testing:
```python
info = """Flight path around MHK starting from Ward Hall
and ending at beverages using a fixed altitude of 200 ft."""
coords = [(-96.5852293,39.1916258,200.0000000),
          (-96.5627603,39.1911535,200.0000000),
          (-96.5686058,39.1943873,200.0000000),
          (-96.5759980,39.1921672,200.0000000),
          (-96.5714061,39.1793939,200.0000000),
          (-96.5657687,39.1801007,200.0000000)]
```

Put your solution in a file named `flight_path.py`.


## Problem 2

Use VisIt and, ideally, it's Python API to visualize a set of actual
flight coordinates stored in the VTK format.  For example, given the
`x`, `y`, and `z` coordinates of some flight path, you can place these
into a file named `points.vtu` by using


```
import pyevtk
coords = np.random.rand(3, 10); x=coords[:,0]; y=coords[:,1]; z=coords[:,2];
pyevtk.hl.pointsToVTK("./points", x, y, z, data={'id': np.arange(0,len(0))})
```

Create a function named `plot_points_visit(fname)`, where `fname+'vtu'` is
the file name containing the data.  This should save a file named
`fname+'.png'` that depicts the scene.
