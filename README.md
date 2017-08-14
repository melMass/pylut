# pylut3

![pylut](http://www.gregcotten.com/files/plot.jpg)

A python module that builds, modifies, visualizes, and converts 3D LUTs from popular .cube and .3dl formats. The end goal for this module is to remove the obfuscation from proprietary LUT formats and provide a way to programmatically manipulate LUTs.

## Installation

	pip install pylut

And to upgrade:

	pip uninstall pylut
	pip install pylut

## Documentation
	
docs viewable at: http://pythonhosted.org/pylut/

## Usage

The idea is that the modifications to a LUT object are non-volatile, meaning that every modification method returns a new LUT object rather than changing the existing object. All sorts of great things can happen!

```python
from pylut import *
lut = LUT.FromLustre3DLFile("/path/to/file.3dl")
lut2 = LUT.FromLustre3DLFile("/path/to/file2.3dl")

print lut.ColorAtLatticePoint(1,2,1)
print lut.ColorAtInterpolatedLatticePoint(1.3,1.5,1.2)
print lut.ColorFromColor(Color(.002,.5,.2344))
print lut.ColorFromColor(Color.FromRGBInteger(14, 1000, 30, bitdepth = 10))

lut3 = lut.CombineWithLUT(lut2)

lut3 *= .5
lut3 -= LUT.FromIdentity(lut3.cubeSize)

lut3 = lut3.ClampColor(Color(0,0,.2),Color(0,0,.4))

lut3 = lut3.Resize(33)
lut3.ToNuke3DLFile("/path/to/destination.3dl")
```


