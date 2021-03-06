# 1D-Photochem-Benchmarks

This repository contains standardized benchmarks for 1-D photochemical models. 

Each folder (e.g. `ModernEarth`) is a separate benchmark, and contains files describing the necessary parameters and model inputs for a photochemical model to complete a benchmark. Following is a description of each file:
- `<foldername>_T_Kzz.txt` contains the temperature and eddy diffusion profiles.
- `<foldername>_flux.txt` contains the stellar flux as a function of wavelength.
- `<foldername>_settings.yaml` contains various planet parameters, and the boundary conditions that should be used for the benchmark.
- `<foldername>_data.yaml` contains measurements of atmospheric composition and surface gas fluxes, if measurements exist.
- `README.md` gives justifications or citations for the selected parameters (e.g. the temperature profile), and contains general notes.

Units of all parameters are [CGS](https://en.wikipedia.org/wiki/Centimetre%E2%80%93gram%E2%80%93second_system_of_units), except when noted otherwise.

## Instructions

Example: `benchmark_results/PhotochemPy`

For each benchmark, implement the settings, boundary conditions, etc. in a photochemical model and compute photochemical equilibrium. Produce the following two files

- `<model-name>_<version-number>_<template-name>_mixingratios.txt`, with the following format. Altitude is in kilometers.

```
alt     H2O      O2       CO2      etc...
1.0     0.02     0.210    3.6e-4
2.0     0.015    0.205    3.6e-4
2.0     0.014    0.201    3.6e-4
etc...   
```


- `<model-name>_<version-number>_<template-name>_surfaceflux.txt`, with the following format.

```
Species          Surface flux (molecules/cm^2/s)    
O                -4.40380e+09                       
O2               8.77371e+11                        
H2O              -1.16115e+14                       
H                -4.45445e+04
etc...
```

## Notes

The `<foldername>_settings.yaml` lists boundary conditions in the following format

```yaml
- name: O2
  lower-boundary:
    mixing-ratio: 0.21
    type: mixing-ratio
  upper-boundary:
    veff: 0.0 # cm/s
    type: effusion velocity
```

These are 4 different `type`s of lower boundary conditions, and 2 types of upper boundary conditions:

```yaml
# Fixed surface mixing ratio.
lower-boundary:
  mixing-ratio: 0.21
  type: mixing-ratio 
  
# Deposition velocity. Flux (molecules/cm^2/s) OUT 
# OF the lower boundary of the model is given by
# [number density of species]*[vdep]
lower-boundary:
  vdep: 1e-4 # cm/s
  type: deposition velocity
  
# Fixed surface flux. Flux INTO the lower boundary of
# the model is [flux]
lower-boundary:
  flux: 1e9 # molecules/cm^2/s
  type: flux
  
# Moses (2001) boundary condition for gas giants.
# Flux (molecules/cm^2/s) OUT OF the bottom of the model is given by
# [surface eddy diffusion coeff]*[surface scale height]^-1*[number density of species]
lower-boundary:
  type: Moses

# Effusion velocity. Flux OUT OF the upper boundary of
# the model is [number density of species]*[veff]
upper-boundary:
  veff: 0.0 # cm/s
  type: effusion velocity
  
# Fixed flux. Flux OUT OF the upper boundary of
# the model is [flux]
upper-boundary:
  flux: 1e9 # molecules/cm^2/s
  type: flux
```

Boundary conditions for molecules NOT specified in `<foldername>_settings.yaml`, should be set to zero deposition velocity and effusion velocity.


