# Observations profile

## Annotated examples of how responses from a profile compliant service will look

### /

Annotated example of a landinpage response that complies with the profile

```json
{
  "title": "E-SOH EDR API",
  "description": "The E-SOH EDR API",
  "links": [
    {
      "href": "https://api.esoh.met.no/",
      "rel": "self",
      "type": "application/json",
      "title": "Landing Page in JSON"
    },
    {
      "href": "https://api.esoh.met.no/docs",
      "rel": "service-doc",
      "type": "text/html",
      "title": "API description in HTML"
    },
    // Landingpage SHALL have a link to openapi describing the service.
    // Note: Each "service" pr. openapi? MIME type for openapi.
    {
      "href": "https://api.esoh.met.no/openapi.json",
      "rel": "service-desc",
      "type": "application/json",
      "title": "API description in JSON"
    },

    // Conformance response SHALL have uri to RODEO profile. 
    // Note: Add an conformance response example with this rule.
    {
      "href": "https://api.esoh.met.no/conformance",
      "rel": "conformance",
      "type": "application/json",
      "title": "Conformance Declaration in JSON"
    },
    {
      "href": "https://api.esoh.met.no/collections",
      "rel": "data",
      "title": "Collections metadata in JSON"
    }
  ],
  "keywords": [
    "weather",
    "temperature",
    "wind",
    "humidity",
    "pressure",
    "clouds",
    "radiation"
  ],
  "provider": {
    "name": "RODEO",
    "url": "https://rodeo-project.eu/"
  },
  "contact": {
    "email": "rodeoproject@fmi.fi"
  }
}
```

### /collections

Annotated example of a collection that complies with the profile

```json
{
    "links": [
      {
        "href": "https://api.esoh.met.no/collections",
        "rel": "self"
      }
    ],
    "collections": [
      {
        "id": "observations",
        "title": "Surface observations from Europe",
        "links": [
          {
            "href": "https://api.esoh.met.no/collections/observations",
            "rel": "data"
          },
          {
            "href": "https://creativecommons.org/licenses/by/4.0/",
            "rel": "license",
            "type": "text/html"
          }
        ],
        "extent": {
          "spatial": {
            "bbox": [
              [
                -73.12083,
                -75.79183333,
                32.9831,
                83.65611
              ]
            ],
            "crs": "EPSG:4326"
          },
          "temporal": {
            "interval": [
              [
                "2024-09-08T09:08:00Z",
                "2024-09-09T09:06:00Z"
              ]
            ],
            "values": [
              "2024-09-08T09:08:00Z/2024-09-09T09:06:00Z"
            ],
            "trs": "datetime"
          }
        },
        // position, area and locations are all required in this profile. A service can support more query types, but a client supporting this profile can ignore them.
        "data_queries": {
          "position": {
            "link": {
              "href": "https://api.esoh.met.no/collections/observations/position",
              "rel": "data",
              "variables": {
                "query_type": "position",
                "output_format": [
                  "CoverageJSON"
                ]
              }
            }
          },
          "area": {
            "link": {
              "href": "https://api.esoh.met.no/collections/observations/area",
              "rel": "data",
              "variables": {
                "query_type": "area",
                "output_format": [
                  "CoverageJSON"
                ]
              }
            }
          },
          "locations": {
            "link": {
              "href": "https://api.esoh.met.no/collections/observations/locations",
              "rel": "data",
              "variables": {
                "query_type": "locations",
                "output_format": [
                  "CoverageJSON"
                ]
              }
            }
          }
        },
        "crs": [
          "WGS84"
        ],
        "output_formats": [
          "CoverageJSON"
        ],
        "parameter_names": {
          // Keys, like "air_pressure:0.0:point:PT0S" should be assumed to contain no structured data.
          "air_pressure:0.0:point:PT0S": {
            "type": "Parameter",
            // Use title to list the parameter in a UI.
            "title": "Air pressure",
            // Optionally, use description to add more information when lisint parameter in a UI.
            "description": "air_pressure at 0.0m PT0S point",
            "unit": {
              "label": "hPa"
            },
            "observedProperty": {
              "id": "https://vocab.nerc.ac.uk/standard_name/air_pressure",
              "label": "air_pressure:0.0:point:PT0S"
            },
            // Always include measurementType
            "measurementType": {
                "method": "point",
                "duration": "PT0S"
            }
          },
          "air_pressure:1.5:mean:PT1H": {
            "type": "Parameter",
            "description": "air_pressure at 1.5m PT1H mean",
            "unit": {
              "label": "hPa"
            },
            "observedProperty": {
              "id": "https://vocab.nerc.ac.uk/standard_name/air_pressure",
              "label": "air_pressure:1.5:mean:PT1H"
            },
            "measurementType": {
                "method": "mean",
                "duration": "PT1H"
            }
          }
        }
      }
    ]
}
```

### CoverageJSON response

An annotated example of a CoverageJSON response from a service compliant with this profile

```json
{
  "type": "CoverageCollection",
  "coverages": [
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        // only domainType PointSeries.
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T09:36:00Z",
              "2024-09-08T09:37:00Z",
              "2024-09-08T09:38:00Z",
              "2024-09-08T09:39:00Z",
              "2024-09-08T09:40:00Z",
              "2024-09-08T09:41:00Z",
              "2024-09-08T09:42:00Z",
              "2024-09-08T09:43:00Z",
              "2024-09-08T09:44:00Z",
              "2024-09-08T09:45:00Z"
            ]
          }
        },
        // The content of referencing must always be exactly this:
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      // The content of parameters should be as close to the content in parameter_names in /collections as possible.
      // Critically, the key for the same parameter needs to be same in both, so that a client can easily match the response to a data query to the metadata in collections.
      "parameters": {
        "relative_humidity:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "relative_humidity at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/relative_humidity",
            "label": {
              "en": "relative_humidity:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "percent"
            }
          }
        }
      },
      "ranges": {
        "relative_humidity:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            1432,
            1,
            1
          ],
          "values": [
            99,
            99,
            99,
            99,
            99,
            99,
            99,
            99,
            99,
            99
          ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T09:36:00Z",
              "2024-09-08T09:37:00Z",
              "2024-09-08T09:38:00Z",
              "2024-09-08T09:39:00Z",
              "2024-09-08T09:40:00Z",
              "2024-09-08T09:41:00Z",
              "2024-09-08T09:42:00Z",
              "2024-09-08T09:43:00Z",
              "2024-09-08T09:44:00Z",
              "2024-09-08T09:45:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        // 
        "air_temperature:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "air_temperature at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
            "label": {
              "en": "air_temperature:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        },
        "rainfall_rate:0.0:mean:PT1M": {
          "type": "Parameter",
          "description": {
            "en": "rainfall_rate at 0.0m PT1M mean"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/rainfall_rate",
            "label": {
              "en": "rainfall_rate:0.0:mean:PT1M"
            }
          },
          "unit": {
            "label": {
              "en": "mm/h"
            }
          }
        }
      },
      "ranges": {
        "air_temperature:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            1430,
            1,
            1
          ],
          "values": [
            6.4000001,
            6.4000001,
            6.4000001,
            6.4000001,
            6.4000001,
            6.4000001,
            6.4000001,
            6.4000001,
            6.4000001,
            6.4000001
          ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T09:36:00Z",
              "2024-09-08T09:37:00Z",
              "2024-09-08T09:38:00Z",
              "2024-09-08T09:39:00Z",
              "2024-09-08T09:40:00Z",
              "2024-09-08T09:41:00Z",
              "2024-09-08T09:42:00Z",
              "2024-09-08T09:43:00Z",
              "2024-09-08T09:44:00Z",
              "2024-09-08T09:45:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1M": {
          "type": "Parameter",
          "description": {
            "en": "surface_downwelling_longwave_flux_in_air at 0.0m PT1M mean"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/surface_downwelling_longwave_flux_in_air",
            "label": {
              "en": "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1M"
            }
          },
          "unit": {
            "label": {
              "en": "W/m2"
            }
          }
        },
        "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1M": {
          "type": "Parameter",
          "description": {
            "en": "surface_downwelling_shortwave_flux_in_air at 0.0m PT1M mean"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/surface_downwelling_shortwave_flux_in_air",
            "label": {
              "en": "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1M"
            }
          },
          "unit": {
            "label": {
              "en": "W/m2"
            }
          }
        }
      },
      "ranges": {
        "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1M": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            1427,
            1,
            1
          ],
          "values": [
            329.899994,
            330,
            330.100006,
            330.299988,
            330.299988,
            330.399994,
            330.399994,
            330.5,
            330.5,
            330.5
          ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T09:40:00Z",
              "2024-09-08T09:50:00Z",
              "2024-09-08T10:00:00Z",
              "2024-09-08T10:10:00Z",
              "2024-09-08T10:20:00Z",
              "2024-09-08T10:30:00Z",
              "2024-09-08T10:40:00Z",
              "2024-09-08T10:50:00Z",
              "2024-09-08T11:00:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        "precipitation_amount:0.0:sum:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "precipitation_amount at 0.0m PT0S sum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
            "label": {
              "en": "precipitation_amount:0.0:sum:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "kg/m2"
            }
          }
        },
        "precipitation_amount:0.0:sum:PT10M": {
          "type": "Parameter",
          "description": {
            "en": "precipitation_amount at 0.0m PT10M sum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
            "label": {
              "en": "precipitation_amount:0.0:sum:PT10M"
            }
          },
          "unit": {
            "label": {
              "en": "kg/m2"
            }
          }
        },
        "wind_from_direction:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "wind_from_direction at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/wind_from_direction",
            "label": {
              "en": "wind_from_direction:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "degrees"
            }
          }
        },
        "wind_speed:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "wind_speed at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/wind_speed",
            "label": {
              "en": "wind_speed:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "m/s"
            }
          }
        },
        "wind_speed_of_gust:0.0:maximum:PT10M": {
          "type": "Parameter",
          "description": {
            "en": "wind_speed_of_gust at 0.0m PT10M maximum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/wind_speed_of_gust",
            "label": {
              "en": "wind_speed_of_gust:0.0:maximum:PT10M"
            }
          },
          "unit": {
            "label": {
              "en": "m/s"
            }
          }
        }
      },
      "ranges": {
        "precipitation_amount:0.0:sum:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            144,
            1,
            1
          ],
          "values": [
            315.867004,
            315.865997,
            315.869995,
            315.869995,
            315.865997,
            315.868988,
            315.856995,
            315.864014,
            315.864014
          ]
        },
        "precipitation_amount:0.0:sum:PT10M": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            144,
            1,
            1
          ],
          "values": [
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0
          ]
        },
        "wind_from_direction:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            144,
            1,
            1
          ],
          "values": [
            105,
            102,
            98.6999969,
            104,
            107,
            104,
            102,
            98,
            91.8000031,
            94
          ]
        },
        "wind_speed:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            144,
            1,
            1
          ],
          "values": [
            4.5,
            4,
            3.9000001,
            3.4000001,
            3.20000005,
            3.70000005,
            4.19999981,
            4.5999999,
            4.30000019,
            3.29999995
          ]
        },
        "wind_speed_of_gust:0.0:maximum:PT10M": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            144,
            1,
            1
          ],
          "values": [
            5.5,
            4.9000001,
            4.9000001,
            4,
            4.0999999,
            5.30000019,
            5.30000019,
            5.69999981,
            5.30000019,
            4.5
            ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T09:40:00Z",
              "2024-09-08T09:50:00Z",
              "2024-09-08T10:00:00Z",
              "2024-09-08T10:10:00Z",
              "2024-09-08T10:20:00Z",
              "2024-09-08T10:30:00Z",
              "2024-09-08T10:40:00Z",
              "2024-09-08T10:50:00Z",
              "2024-09-08T11:00:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        "cloud_area_fraction:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "cloud_area_fraction at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/cloud_area_fraction",
            "label": {
              "en": "cloud_area_fraction:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "oktas"
            }
          }
        },
        "latitude:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "latitude at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/latitude",
            "label": {
              "en": "latitude:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "degrees"
            }
          }
        },
        "longitude:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "longitude at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/longitude",
            "label": {
              "en": "longitude:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "degrees"
            }
          }
        }
      },
      "ranges": {
        "cloud_area_fraction:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            141,
            1,
            1
          ],
          "values": [
            8,
            8,
            8,
            8,
            8,
            8,
            8,
            8,
            8,
            8
          ]
        },
        "latitude:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            141,
            1,
            1
          ],
          "values": [
            70.9395981,
            70.9395981,
            70.9395981,
            70.9395981,
            70.9395981,
            70.9395981,
            70.9395981,
            70.9395981,
            70.9395981,
            70.9395981          
          ]
        },
        "longitude:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            141,
            1,
            1
          ],
          "values": [
            -8.66905022,
            -8.66905022,
            -8.66905022,
            -8.66905022,
            -8.66905022,
            -8.66905022,
            -8.66905022,
            -8.66905022,
            -8.66905022,
            -8.66905022
          ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T10:00:00Z",
              "2024-09-08T11:00:00Z",
              "2024-09-08T12:00:00Z",
              "2024-09-08T13:00:00Z",
              "2024-09-08T14:00:00Z",
              "2024-09-08T15:00:00Z",
              "2024-09-08T16:00:00Z",
              "2024-09-08T17:00:00Z",
              "2024-09-08T18:00:00Z",
              "2024-09-08T19:00:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        "air_temperature:0.0:maximum:PT1H": {
          "type": "Parameter",
          "description": {
            "en": "air_temperature at 0.0m PT1H maximum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
            "label": {
              "en": "air_temperature:0.0:maximum:PT1H"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        },
        "air_temperature:0.0:minimum:PT1H": {
          "type": "Parameter",
          "description": {
            "en": "air_temperature at 0.0m PT1H minimum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
            "label": {
              "en": "air_temperature:0.0:minimum:PT1H"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        },
        "precipitation_amount:0.0:sum:PT1H": {
          "type": "Parameter",
          "description": {
            "en": "precipitation_amount at 0.0m PT1H sum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
            "label": {
              "en": "precipitation_amount:0.0:sum:PT1H"
            }
          },
          "unit": {
            "label": {
              "en": "kg/m2"
            }
          }
        },
        "soil_temperature:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "soil_temperature at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/soil_temperature",
            "label": {
              "en": "soil_temperature:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        },
        "surface_air_pressure:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "surface_air_pressure at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/surface_air_pressure",
            "label": {
              "en": "surface_air_pressure:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "hPa"
            }
          }
        },
        "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1H": {
          "type": "Parameter",
          "description": {
            "en": "surface_downwelling_longwave_flux_in_air at 0.0m PT1H mean"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/surface_downwelling_longwave_flux_in_air",
            "label": {
              "en": "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1H"
            }
          },
          "unit": {
            "label": {
              "en": "W/m2"
            }
          }
        },
        "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1H": {
          "type": "Parameter",
          "description": {
            "en": "surface_downwelling_shortwave_flux_in_air at 0.0m PT1H mean"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/surface_downwelling_shortwave_flux_in_air",
            "label": {
              "en": "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1H"
            }
          },
          "unit": {
            "label": {
              "en": "W/m2"
            }
          }
        },
        "surface_temperature:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "surface_temperature at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/surface_temperature",
            "label": {
              "en": "surface_temperature:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        },
        "tendency_of_surface_air_pressure:0.0:point:PT3H": {
          "type": "Parameter",
          "description": {
            "en": "tendency_of_surface_air_pressure at 0.0m PT3H point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/tendency_of_surface_air_pressure",
            "label": {
              "en": "tendency_of_surface_air_pressure:0.0:point:PT3H"
            }
          },
          "unit": {
            "label": {
              "en": "hPa"
            }
          }
        },
        "wind_from_direction:0.0:maximum:PT1H": {
          "type": "Parameter",
          "description": {
            "en": "wind_from_direction at 0.0m PT1H maximum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/wind_from_direction",
            "label": {
              "en": "wind_from_direction:0.0:maximum:PT1H"
            }
          },
          "unit": {
            "label": {
              "en": "degrees"
            }
          }
        },
        "wind_speed:0.0:maximum:PT1H": {
          "type": "Parameter",
          "description": {
            "en": "wind_speed at 0.0m PT1H maximum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/wind_speed",
            "label": {
              "en": "wind_speed:0.0:maximum:PT1H"
            }
          },
          "unit": {
            "label": {
              "en": "m/s"
            }
          }
        },
        "wind_speed_of_gust:0.0:maximum:PT1H": {
          "type": "Parameter",
          "description": {
            "en": "wind_speed_of_gust at 0.0m PT1H maximum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/wind_speed_of_gust",
            "label": {
              "en": "wind_speed_of_gust:0.0:maximum:PT1H"
            }
          },
          "unit": {
            "label": {
              "en": "m/s"
            }
          }
        }
      },
      "ranges": {
        "air_temperature:0.0:maximum:PT1H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            6,
            6.30000019,
            7.0999999,
            7.4000001,
            7.30000019,
            7.4000001,
            7.4000001,
            7.69999981,
            7.80000019
          ]
        },
        "air_temperature:0.0:minimum:PT1H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            5.80000019,
            6,
            6.30000019,
            7,
            7.0999999,
            7,
            7.30000019,
            7.30000019,
            7.19999981,
            7
          ]
        },
        "precipitation_amount:0.0:sum:PT1H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0
          ]
        },
        "soil_temperature:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            5.5999999,
            6.0999999,
            6.69999981,
            7.5,
            7.80000019,
            7.69999981,
            7.5,
            7.30000019,
            7,
            6.80000019
          ]
        },
        "surface_air_pressure:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            999.400024,
            999.099976,
            999,
            998.5,
            998,
            997.400024,
            996.599976,
            995.5,
            995.5
          ]
        },
        "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            329.100006,
            325.899994,
            327.399994,
            318.200012,
            308.799988,
            320.899994,
            319.5,
            319.299988,
            326,
            323.899994
          ]
        },
        "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            40.2000008,
            98.4000015,
            121.099998,
            179.699997,
            106.5,
            63.5,
            69.6999969,
            64.4000015,
            19.7999992,
            15.6000004

          ]
        },
        "surface_temperature:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            6.39099979,
            7.13800001,
            7.84299994,
            8.86999989,
            7.7249999,
            7.58199978,
            7.08400011,
            6.75,
            6.38100004,
            6.25199986
          ]
        },
        "tendency_of_surface_air_pressure:0.0:point:PT3H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            0.100000001,
            0.5,
            0.699999988,
            0.899999976,
            1.10000002,
            1.60000002,
            1.79999995,
            2.5,
            1.79999995,
            1.70000005
          ]
        },
        "wind_from_direction:0.0:maximum:PT1H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            99.3000031,
            91.8000031,
            84.8000031,
            81.0999985,
            87.1999969,
            84.9000015,
            348.200012,
            339.5,
            345.899994,
            340.700012
          ]
        },
        "wind_speed:0.0:maximum:PT1H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            4.4000001,
            4.9000001,
            4.5999999,
            4.30000019,
            3.20000005,
            2.4000001,
            4.19999981,
            8.39999962,
            9.5,
            10.5
          ]
        },
        "wind_speed_of_gust:0.0:maximum:PT1H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            24,
            1,
            1
          ],
          "values": [
            5.19999981,
            5.69999981,
            5.5,
            5,
            3.70000005,
            3.29999995,
            5.5999999,
            11.1000004,
            12.5,
            15.5
          ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T14:50:00Z",
              "2024-09-09T04:50:00Z",
              "2024-09-09T05:20:00Z",
              "2024-09-09T05:50:00Z",
              "2024-09-09T06:20:00Z",
              "2024-09-09T06:50:00Z",
              "2024-09-09T07:20:00Z",
              "2024-09-09T07:50:00Z",
              "2024-09-09T08:20:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        "dew_point_temperature:0.0:point:PT0S": {
          "type": "Parameter",
          "description": {
            "en": "dew_point_temperature at 0.0m PT0S point"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/dew_point_temperature",
            "label": {
              "en": "dew_point_temperature:0.0:point:PT0S"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        }
      },
      "ranges": {
        "dew_point_temperature:0.0:point:PT0S": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            9,
            1,
            1
          ],
          "values": [
            6,
            4,
            4,
            4,
            4,
            4,
            4,
            5,
            5
          ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T18:00:00Z",
              "2024-09-09T06:00:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        "air_temperature:0.0:maximum:PT12H": {
          "type": "Parameter",
          "description": {
            "en": "air_temperature at 0.0m PT12H maximum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
            "label": {
              "en": "air_temperature:0.0:maximum:PT12H"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        },
        "air_temperature:0.0:minimum:PT12H": {
          "type": "Parameter",
          "description": {
            "en": "air_temperature at 0.0m PT12H minimum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
            "label": {
              "en": "air_temperature:0.0:minimum:PT12H"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        },
        "precipitation_amount:0.0:sum:PT12H": {
          "type": "Parameter",
          "description": {
            "en": "precipitation_amount at 0.0m PT12H sum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
            "label": {
              "en": "precipitation_amount:0.0:sum:PT12H"
            }
          },
          "unit": {
            "label": {
              "en": "kg/m2"
            }
          }
        }
      },
      "ranges": {
        "air_temperature:0.0:maximum:PT12H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            2,
            1,
            1
          ],
          "values": [
            7.9000001,
            7.5
          ]
        },
        "air_temperature:0.0:minimum:PT12H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            2,
            1,
            1
          ],
          "values": [
            4.69999981,
            4.80000019
          ]
        },
        "precipitation_amount:0.0:sum:PT12H": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            2,
            1,
            1
          ],
          "values": [
            0,
            1.89999998
          ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-08T23:00:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        "air_temperature:0.0:mean:P1D": {
          "type": "Parameter",
          "description": {
            "en": "air_temperature at 0.0m P1D mean"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
            "label": {
              "en": "air_temperature:0.0:mean:P1D"
            }
          },
          "unit": {
            "label": {
              "en": "degC"
            }
          }
        },
        "relative_humidity:0.0:mean:P1D": {
          "type": "Parameter",
          "description": {
            "en": "relative_humidity at 0.0m P1D mean"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/relative_humidity",
            "label": {
              "en": "relative_humidity:0.0:mean:P1D"
            }
          },
          "unit": {
            "label": {
              "en": "percent"
            }
          }
        }
      },
      "ranges": {
        "air_temperature:0.0:mean:P1D": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            1,
            1,
            1
          ],
          "values": [
            6.4000001
          ]
        },
        "relative_humidity:0.0:mean:P1D": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            1,
            1,
            1
          ],
          "values": [
            88.1999969
          ]
        }
      }
    },
    {
      "type": "Coverage",
      "domain": {
        "type": "Domain",
        "domainType": "PointSeries",
        "axes": {
          "x": {
            "values": [
              -8.669
            ]
          },
          "y": {
            "values": [
              70.9394
            ]
          },
          "t": {
            "values": [
              "2024-09-09T06:00:00Z"
            ]
          }
        },
        "referencing": [
          {
            "coordinates": [
              "y",
              "x"
            ],
            "system": {
              "type": "GeographicCRS",
              "id": "http://www.opengis.net/def/crs/EPSG/0/4326"
            }
          },
          {
            "coordinates": [
              "t"
            ],
            "system": {
              "type": "TemporalRS",
              "calendar": "Gregorian"
            }
          }
        ]
      },
      "parameters": {
        "precipitation_amount:0.0:sum:P1D": {
          "type": "Parameter",
          "description": {
            "en": "precipitation_amount at 0.0m P1D sum"
          },
          "observedProperty": {
            "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
            "label": {
              "en": "precipitation_amount:0.0:sum:P1D"
            }
          },
          "unit": {
            "label": {
              "en": "kg/m2"
            }
          }
        }
      },
      "ranges": {
        "precipitation_amount:0.0:sum:P1D": {
          "type": "NdArray",
          "dataType": "float",
          "axisNames": [
            "t",
            "y",
            "x"
          ],
          "shape": [
            1,
            1,
            1
          ],
          "values": [
            1.89999998
          ]
        }
      }
    }
  ],
  "parameters": {
    "air_temperature:0.0:maximum:PT12H": {
      "type": "Parameter",
      "description": {
        "en": "air_temperature at 0.0m PT12H maximum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
        "label": {
          "en": "air_temperature:0.0:maximum:PT12H"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "air_temperature:0.0:maximum:PT1H": {
      "type": "Parameter",
      "description": {
        "en": "air_temperature at 0.0m PT1H maximum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
        "label": {
          "en": "air_temperature:0.0:maximum:PT1H"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "air_temperature:0.0:mean:P1D": {
      "type": "Parameter",
      "description": {
        "en": "air_temperature at 0.0m P1D mean"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
        "label": {
          "en": "air_temperature:0.0:mean:P1D"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "air_temperature:0.0:minimum:PT12H": {
      "type": "Parameter",
      "description": {
        "en": "air_temperature at 0.0m PT12H minimum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
        "label": {
          "en": "air_temperature:0.0:minimum:PT12H"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "air_temperature:0.0:minimum:PT1H": {
      "type": "Parameter",
      "description": {
        "en": "air_temperature at 0.0m PT1H minimum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
        "label": {
          "en": "air_temperature:0.0:minimum:PT1H"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "air_temperature:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "air_temperature at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/air_temperature",
        "label": {
          "en": "air_temperature:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "cloud_area_fraction:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "cloud_area_fraction at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/cloud_area_fraction",
        "label": {
          "en": "cloud_area_fraction:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "oktas"
        }
      }
    },
    "dew_point_temperature:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "dew_point_temperature at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/dew_point_temperature",
        "label": {
          "en": "dew_point_temperature:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "latitude:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "latitude at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/latitude",
        "label": {
          "en": "latitude:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "degrees"
        }
      }
    },
    "longitude:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "longitude at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/longitude",
        "label": {
          "en": "longitude:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "degrees"
        }
      }
    },
    "precipitation_amount:0.0:sum:P1D": {
      "type": "Parameter",
      "description": {
        "en": "precipitation_amount at 0.0m P1D sum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
        "label": {
          "en": "precipitation_amount:0.0:sum:P1D"
        }
      },
      "unit": {
        "label": {
          "en": "kg/m2"
        }
      }
    },
    "precipitation_amount:0.0:sum:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "precipitation_amount at 0.0m PT0S sum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
        "label": {
          "en": "precipitation_amount:0.0:sum:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "kg/m2"
        }
      }
    },
    "precipitation_amount:0.0:sum:PT10M": {
      "type": "Parameter",
      "description": {
        "en": "precipitation_amount at 0.0m PT10M sum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
        "label": {
          "en": "precipitation_amount:0.0:sum:PT10M"
        }
      },
      "unit": {
        "label": {
          "en": "kg/m2"
        }
      }
    },
    "precipitation_amount:0.0:sum:PT12H": {
      "type": "Parameter",
      "description": {
        "en": "precipitation_amount at 0.0m PT12H sum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
        "label": {
          "en": "precipitation_amount:0.0:sum:PT12H"
        }
      },
      "unit": {
        "label": {
          "en": "kg/m2"
        }
      }
    },
    "precipitation_amount:0.0:sum:PT1H": {
      "type": "Parameter",
      "description": {
        "en": "precipitation_amount at 0.0m PT1H sum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/precipitation_amount",
        "label": {
          "en": "precipitation_amount:0.0:sum:PT1H"
        }
      },
      "unit": {
        "label": {
          "en": "kg/m2"
        }
      }
    },
    "rainfall_rate:0.0:mean:PT1M": {
      "type": "Parameter",
      "description": {
        "en": "rainfall_rate at 0.0m PT1M mean"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/rainfall_rate",
        "label": {
          "en": "rainfall_rate:0.0:mean:PT1M"
        }
      },
      "unit": {
        "label": {
          "en": "mm/h"
        }
      }
    },
    "relative_humidity:0.0:mean:P1D": {
      "type": "Parameter",
      "description": {
        "en": "relative_humidity at 0.0m P1D mean"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/relative_humidity",
        "label": {
          "en": "relative_humidity:0.0:mean:P1D"
        }
      },
      "unit": {
        "label": {
          "en": "percent"
        }
      }
    },
    "relative_humidity:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "relative_humidity at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/relative_humidity",
        "label": {
          "en": "relative_humidity:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "percent"
        }
      }
    },
    "soil_temperature:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "soil_temperature at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/soil_temperature",
        "label": {
          "en": "soil_temperature:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "surface_air_pressure:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "surface_air_pressure at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/surface_air_pressure",
        "label": {
          "en": "surface_air_pressure:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "hPa"
        }
      }
    },
    "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1H": {
      "type": "Parameter",
      "description": {
        "en": "surface_downwelling_longwave_flux_in_air at 0.0m PT1H mean"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/surface_downwelling_longwave_flux_in_air",
        "label": {
          "en": "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1H"
        }
      },
      "unit": {
        "label": {
          "en": "W/m2"
        }
      }
    },
    "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1M": {
      "type": "Parameter",
      "description": {
        "en": "surface_downwelling_longwave_flux_in_air at 0.0m PT1M mean"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/surface_downwelling_longwave_flux_in_air",
        "label": {
          "en": "surface_downwelling_longwave_flux_in_air:0.0:mean:PT1M"
        }
      },
      "unit": {
        "label": {
          "en": "W/m2"
        }
      }
    },
    "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1H": {
      "type": "Parameter",
      "description": {
        "en": "surface_downwelling_shortwave_flux_in_air at 0.0m PT1H mean"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/surface_downwelling_shortwave_flux_in_air",
        "label": {
          "en": "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1H"
        }
      },
      "unit": {
        "label": {
          "en": "W/m2"
        }
      }
    },
    "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1M": {
      "type": "Parameter",
      "description": {
        "en": "surface_downwelling_shortwave_flux_in_air at 0.0m PT1M mean"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/surface_downwelling_shortwave_flux_in_air",
        "label": {
          "en": "surface_downwelling_shortwave_flux_in_air:0.0:mean:PT1M"
        }
      },
      "unit": {
        "label": {
          "en": "W/m2"
        }
      }
    },
    "surface_temperature:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "surface_temperature at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/surface_temperature",
        "label": {
          "en": "surface_temperature:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "degC"
        }
      }
    },
    "tendency_of_surface_air_pressure:0.0:point:PT3H": {
      "type": "Parameter",
      "description": {
        "en": "tendency_of_surface_air_pressure at 0.0m PT3H point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/tendency_of_surface_air_pressure",
        "label": {
          "en": "tendency_of_surface_air_pressure:0.0:point:PT3H"
        }
      },
      "unit": {
        "label": {
          "en": "hPa"
        }
      }
    },
    "wind_from_direction:0.0:maximum:PT1H": {
      "type": "Parameter",
      "description": {
        "en": "wind_from_direction at 0.0m PT1H maximum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/wind_from_direction",
        "label": {
          "en": "wind_from_direction:0.0:maximum:PT1H"
        }
      },
      "unit": {
        "label": {
          "en": "degrees"
        }
      }
    },
    "wind_from_direction:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "wind_from_direction at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/wind_from_direction",
        "label": {
          "en": "wind_from_direction:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "degrees"
        }
      }
    },
    "wind_speed:0.0:maximum:PT1H": {
      "type": "Parameter",
      "description": {
        "en": "wind_speed at 0.0m PT1H maximum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/wind_speed",
        "label": {
          "en": "wind_speed:0.0:maximum:PT1H"
        }
      },
      "unit": {
        "label": {
          "en": "m/s"
        }
      }
    },
    "wind_speed:0.0:point:PT0S": {
      "type": "Parameter",
      "description": {
        "en": "wind_speed at 0.0m PT0S point"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/wind_speed",
        "label": {
          "en": "wind_speed:0.0:point:PT0S"
        }
      },
      "unit": {
        "label": {
          "en": "m/s"
        }
      }
    },
    "wind_speed_of_gust:0.0:maximum:PT10M": {
      "type": "Parameter",
      "description": {
        "en": "wind_speed_of_gust at 0.0m PT10M maximum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/wind_speed_of_gust",
        "label": {
          "en": "wind_speed_of_gust:0.0:maximum:PT10M"
        }
      },
      "unit": {
        "label": {
          "en": "m/s"
        }
      }
    },
    "wind_speed_of_gust:0.0:maximum:PT1H": {
      "type": "Parameter",
      "description": {
        "en": "wind_speed_of_gust at 0.0m PT1H maximum"
      },
      "observedProperty": {
        "id": "https://vocab.nerc.ac.uk/standard_name/wind_speed_of_gust",
        "label": {
          "en": "wind_speed_of_gust:0.0:maximum:PT1H"
        }
      },
      "unit": {
        "label": {
          "en": "m/s"
        }
      }
    }
  }
}
```
