# MAXAR_nonvisual_geometry

## Contributors

* Richard Mooreland
* Björn Blissing, [@bjornblissing](https://github.com/bjornblissing)

## Status

Version 1.0

## Dependencies

Written against the glTF 2.0 spec.

## Overview

In gaming and simulation engines, high resolution 3D models are often paired
with nonvisual versions of the model that are optimized for other purposes than
rendering and visualization. This extension to glTF enables designation of
meshes as nonvisual representations of nodes.  Each primitive of the nonvisual
mesh specifies its intended usage.

## Shape of non visual geometry

| Shape        | Description | Allowed `mesh.primitive.mode` |
| ------------ | ----------- | ------------------------------|
| `points`     | One or more points. | `0`- POINTS |
| `path`       | One polyline, may be self intersecting. | `1` - LINES, `2` - LINE_LOOP, `3` - LINE_STRIP _(for mode `1` only two vertex points are allowed)_.|
| `surface`    | One non-self intersecting triangulated surface. | `4` - TRIANGLES, `5` - TRIANGLE_STRIP, `6` - TRIANGLE_FAN  |
| `volume`     | One closed, convex, triangulated polyhedron. | `4` - TRIANGLES, `5` - TRIANGLE_STRIP |

## Types of Nonvisual Meshes

Commonly used types of nonvisual meshes include:

| Type        | Description |
| ----------- | ----------- |
| `collision` | Geometry used for collision detection and simulation |
| `roadway`   | Walkable or drivable surface |
| `ladder`    | One line to convey where a player may enter/exit a ladder |
| `action`    | Geometry used to trigger the articulations assigned to this node |

## Adding Nonvisual Meshes

The following example illustrates how a node can designate a mesh as container for the non-visual representation. This mesh can contain several different nonvisual representations of the mesh:

```json
"nodes": [{
    "name": "Detailed Building",
    "mesh": 0,
    "extensions": {
      "MAXAR_nonvisual_geometry": {
        "mesh": 1
      }
    }
  }
],
"meshes": [{
    "name": "Detailed Building Mesh",
    "primitives": [{
        "attributes": {
          "POSITION": 0,
          "NORMAL": 1
        },
        "indices": 2
      }
    ]
  }, {
    "name": "Nonvisual Building Mesh",
    "primitives": [{
        "attributes": {
          "POSITION": 3
        },
        "indices": 4,
        "extensions": {
          "MAXAR_nonvisual_geometry": {
            "shape": "surface",
            "type": "roadway"
          }
        }
      }, {
        "attributes": {
          "POSITION": 5
        },
        "indices": 6,
        "mode": 1,
        "extensions": {
          "MAXAR_nonvisual_geometry": {
            "shape": "path",
            "type": "ladder"
          }
        }
      }, {
        "attributes": {
          "POSITION": 7
        },
        "indices": 8,
        "extensions": {
          "MAXAR_nonvisual_geometry": {
            "shape": "volume",
            "type": "collision"
          }
        }
      }
    ]
  }
]
```

## Optional vs. Required

This extension is considered optional, meaning it should be placed in the glTF
root's `extensionsUsed` list, but not in the `extensionsRequired` list.

## Schema Updates

- **glTF node extension JSON schema**: [node.MAXAR_nonvisual_geometry.schema.json](schema/node.MAXAR_nonvisual_geometry.schema.json)
- **glTF mesh primitive extension JSON schema**: [mesh.primitive.MAXAR_nonvisual_geometry.schema.json](schema/mesh.primitive.MAXAR_nonvisual_geometry.schema.json)
