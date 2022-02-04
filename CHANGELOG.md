# Changelog

All notable changes to this data set will be documented here.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Unreleased

## [2.0.0] - 2022-02-04

### Changed

- Reorganized ``solute`` and ``solute.solvent`` to ``heterogeneous`` and ``homogeneous``.
- Moved selected ABCluster structures into the ``abc`` folders instead of having them separate.

### Added

- Methanol 20mers from Pires & Deturi (DOI [10.1021/ct600348x](https://doi.org/10.1021/ct600348x)) and Yao et al (DOI [10.1063/1.4973380](https://doi.org/10.1063/1.4973380)).
- Packmol generated structures of 30h2o, 112h2o, 140h2o, 30mecn, 39mecn, 30meoh, 50meoh, and 62meoh.
- ORCA MP2/def2-TZVP energy+gradient calculation of Yoo et al. boat-b 16mer.
- Methanol 4-6mer minima from Boyd et al. (DOI [10.1021/ct6002912](https://doi.org/10.1021/ct6002912)) with MP2/def2-TZVP engrads.
- Acetonitrile 4-6mer minima from Malloum et al. (DOI: [10.1002/qua.26222](https://doi.org/10.1002/qua.26222)) with MP2/def2-TZVP engrads.
- Water 16mer minima from Yoo et al. (DOI: [10.1021/jz101245s](https://doi.org/10.1021/jz101245s)) with RI-MP2/def2-TZVP engrad.
- Water 4-6mer minima from Temelso et al. (DOI: [10.1021/jp2069489](https://doi.org/10.1021/jp2069489)) with MP2/def2-TZVP engrads.
- 20 Angstrom box of water from GROMACS solvate.

### Removed

- Moved 12h2o.su.etal monomers, dimers, and trimers to [another repository](https://github.com/keithgroup/mbgdml-h2o-meoh-mecn-engrads).

## [1.0.0] - 2021-01-17

- Initial release!
