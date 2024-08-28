# EDR-profiles

## Purpose

The purpose of these EDR profiles is to constrain the OGC-API EDR standard such that clients can consume meteorological data from multiple EDR WebAPI services without having to write custom code for each of those WebAPIs.

The profiles are meant to be used as described here: https://github.com/opengeospatial/ogcapi-environmental-data-retrieval/issues/404.

## Approach

Build an OpenAPI specification for each profile, along with human readable documentation and an automatic validation tool.

The OpenAPI specification can be used to validate that a service is compliant with the profile. It could potentially also be used to generate client and server code in multiple programming languages.

We want as few profiles as possible. However, if there is a need for more than one meteorological EDR profile, it probably makes sense to make separate profiles based on the data type, e.g observations, forecasts, radar etc.

The work is 100% open source and the goal is to have a community driven effort that can be used by everyone.

## Roadmap

A tentative plan for what to do when.

### Starting august 2024: Observations data

Define the profile needs for meteorological ground observations data. Possible as a separate profile.

First, we want to tackle the metadata about parameters, units and coordinate systems, e.g decide on which vocabularies to use.

Then, work more directly on the OpenAPI specification, with things like:

- the details of the content of `/collections`.
- which queries to support
- response formats for the data queries.

### Late 2024: Forecast data

Define the profile needs for meteorological weather forecast data. Possible as a separate profile.
