# 1D-Photochem-Benchmarks

This repository contains standardized benchmarks for 1-D photochemical models. 

Each folder (e.g. `PreindustrialEarth`) is a separate benchmark, and contains files describing the necessary parameters and model inputs for a photochemical model to complete a benchmark. Following is a description of each file:
- `<foldername>_T_Kzz.txt` contains the temperature and altitude profiles.
- `<foldername>_flux.txt` contains the stellar flux as a function of wavelength.
- `<foldername>.yaml` contains various planet parameters, and the boundary conditions that should be used for the benchmark. Also, this file contains measurements of atmospheric composition and surface gas fluxes, if measurements exist.
- `README.md` gives justifications or citations for the selected parameters (e.g. the temperature profile), and contains general notes.
