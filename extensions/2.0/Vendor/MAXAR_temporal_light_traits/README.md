# MAXAR\_temporal\_light\_traits

## Contributors

* Richard Moreland, Maxar
* Björn Blissing, Maxar, [@bjornblissing](https://twitter.com/bjornblissing)

## Status

Draft

## Dependencies

Written against the glTF 2.0 spec. Extends the `KHR_lights_punctual` `light` concept.

## Overview

This extension defines a set of traits to describe the animated aspects of a light. It builds upon the `KHR_lights_punctual` extension's description of a light.

## Adding Traits to Lights

The following sample coarsely demonstrates how the two extensions work together:

```javascript
"extensions": {
    "KHR_lights_punctual": {
        "lights": [
            {
                "type": "point",
                // ...
                "extensions": {
                    "MAXAR_temporal_light_traits": {
                        "flashing": {
                            "duty": 0.75,
                            "frequency": 1.0,
                            "waveform": "square"
                        }
                    }
                }
            }
        ]
    }
}
```

## Trait Types

A light can opt to not use the extension at all (meaning the light does not change with time), or it can use any one of the traits defined below.  Other possible traits could include more complex flashing patterns such as morse code patterns.

### Flashing

The `"flashing"` trait describes a simple flashing pattern that can be characterized by a waveform type and frequency.

| Property      | Description | Required |
|:--------------|:------------|:---------|
| `amplitudeOffset` | Offset amplitude from default range of `(0.0, 1.0)` | No, Default: `0.0` |
| `amplitudeScale` | Scale amplitude from default range of `(0.0, 1.0)` | No, Default: `1.0` |
| `duty`        | Portion of period the light is on as normalized value `(0.0, 1.0)`, only applicable for `"square"` waveforms | No, Default: `0.5` |
| `frequency`   | Frequency of the waveform (Hz), only positive values are allowed  | Yes |
| `phaseOffset` | Frequency offset (seconds)  | No, Default: `0.0` |
| `waveform`    | Shape of waveform, one of `"sine"`, `"square"`, `"triangle"` | Yes |