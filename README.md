# Solute-solvent clusters [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5975478.svg)](https://doi.org/10.5281/zenodo.5975478)

This work provides a database of solute, solvent, and solute-solvent clusters and energies.
Clusters are curated from literature or from global optimization codes.
ABCluster is typically used with the CHARMM force field to generate several low-energy structures.
ORCA is then used to optimize structures and calculate electronic energies and free energy corrections.
This data set is not exhaustive; data is included as the Keith group's research interests evolve.

## Manifest

Data is organized into the following directories.

- `clusters`: Structures and output files from optimizations and electronic structure calculations.
- `forcefields`: Parameters used for global optimization calculations.
- `benchmark`: Calculations used to benchmark global optimization codes.

Structures are typically stored in a XYZ format.
[Quantum chemical JSON](https://github.com/keithgroup/group-scripts/tree/master/examples/qjson-creator) or raw-text output files are provided for ABCluster and ORCA calculations.

### Species

Clusters that only contain one chemical species (``homogeneous``): water, acetonitrile, and methanol.

Clusters containing two or mores chemical species (``heterogeneous``) are shown in the table below.

| Solvents | Solutes |
| :---: | :--- |
| Water | H<sup>+</sup>, Li<sup>+</sup>, Na<sup>+</sup>, K<sup>+</sup>, Ca<sup>2+</sup> <br> CO<sub>3</sub><sup>2–</sup>, SO<sub>4</sub><sup>2–</sup> |
| Methanol | Cl<sup>–</sup> |
| Acetonitrile | Na<sup>+</sup> |
| Water+Methanol | Na<sup>+</sup> |
| Water+Acetonitrile | Na<sup>+</sup> |

## Global optimization

Many of these structures involve clusters of solute and/or solvent molecules.
Global optimization codes are often used to identify low-energy structures for the system of interest.

### ABCLuster

A [package](http://www.zhjun-sci.com/software-abcluster-download.php) that searchers the global and local minima of atomic and molecular clusters using the artificial bee colony algorithm with the CHARMM force field.
This black-box package is used to identify multiple low-energy structures to then be further optimized with quantum mechanical methods.

#### Settings

For simplicity, common settings for ABCluster calculations are described here and are used throughout the data set.

- ``default``: population size: 500, maximum cycles: 1000, scouts: 15.

## Conventions

### File names

Each file is named following this convention: `<structure>-<calculation>-<options>-<iteration>`.
Information within each `<>` block is generally separated by a period; this minimizes the width of the file name.
An underscore is sometimes used with information that could be positive or negative, although this is avoided whenever possible.
Lowercase is used to speed up navigation with a terminal.

- `<structure>`: A human-readable, unique label for the structure involved.
  It should also specify refinements (i.e., optimizations) to represent a breadcrumb trail.
  <br><br>
  **Example**
  The third lowest energy water cluster with four molecules predicted from ABCluster would be `4h2o.abc2`.
  Note, we use zero indexing here, meaning that the lowest-energy structure would be `4h2o.abc0`.
  If we then optimized `4h2o.abc2` with B3LYP/def2-TZVP with and without the CPCM solvent model we would have another two structures: `4h2o.abc2.b3lyp.cpcm` and `4h2o.abc2.b3lyp`, respectively.
  Usually, we do not include common information shared between files, so `def2tzvp` is left out.
  <br><br>
  Other common prefixes include `mol` for specifying the molecule partitions from a larger cluster and `iter` for iteration.
  For example, a dimer structure with the first and fourth molecule from (H<sub>2</sub>O)<sub>12</sub> would be `12h2o.mol0,3.xyz` (we start from zero).
  Structures from the final calculation of a line of restarts does not need to include the `r` in the structure labels (discussed next).

- `<calculation>`: Specification of the program and calculation type for output files.
  Restarts should be specified by appending a `r`.
  <br><br>
  **Example**
  Suppose the optimizations were performed in ORCA, and the first optimization did not converge and had to be restarted.
  The output file of the first optimization would be `orca.opt` and `orca.opt.r` for the restart.
  If a second restart was required, another `r` would just be appended like so: `orca.opt.rr`.
  Sometimes program versions can be added: for example, `orca3.opt` and `orca42.opt` (for ORCA version 4.2).

- `<options>`: Calculation specifications or parameters.
  Usually only the major options are included and is left up to the contributor.
  <br><br>
  **Example**
  The output file for our B3LYP/def2-TZVP optimization with D3BJ dispersion corrections and tight self-consistent field convergence criteria would be at most `b3lyp.d3bj.def2tzvp.tightscf`, but could be shortened to just `b3lyp.def2tzvp`.
  Punctuations or spaces specified in options should be removed (e.g., `def2tzvp` not `def2-tzvp` and `tightscf` not `tight scf` or `tight.scf`).
  The order generally does not matter, but should either follow community standards or a top-down approach to help file ordering.
  For example, DFT calculation properties are typically specified as B3LYP-D3BJ/def2-TZVP, so we would put `d3bj` before `def2tzvp`.
  Sometimes, commonly used options can be grouped together under a user-defined label defined here.

- `<iteration>`:
  An `iter` label should be used for calculations where multiple calculations are likely, like ABCluster calculations.
  This avoids the unfortunate situation where many files have to be renamed to include an `iter1` label.

While this often leads to longer file names, we believe that this provides quicker navigation and reduces human errors such as overwriting and misinterpreting data.

### Directory organization

Structures and calculations are organized by system (solvent and solute-solvent structures), the chemical species in the cluster, and the number of solvent molecules.
There should be a directory for every base structure and source (e.g., global optimizations).
The following file tree is an example of a files for a water tetramer.

```text
.
├── 4h2o-abc
│   ├── 4h2o-abc.rigidmol-charmm36.default-1-lm
│   │   ├── 4h2o.abc0.iter1.xyz
│   │   ├── 4h2o.abc1.iter1.xyz
│   │   ├── 4h2o.abc2.iter1.xyz
        ...
│   ├── 4h2o-abc.rigidmol-charmm36.default-1.out
│   ├── 4h2o-abc.rigidmol-charmm36.default-2-lm
│   │   ├── 4h2o.abc0.iter2.xyz
│   │   ├── 4h2o.abc1.iter2.xyz
│   │   ├── 4h2o.abc2.iter2.xyz
        ...
│   └── 4h2o-abc.rigidmol-charmm36.default-2.out
├── 4h2o.abc0.iter1
│   ├── 4h2o.abc0.iter1.b3lyp.smd.xyz
│   ├── 4h2o.abc0.iter1.b3lyp.xyz
│   └── 4h2o.abc0.iter1-calcs
│       ├── 4h2o.abc0.iter1-freq
│       │   ├── 4h2o.abc0.iter1.b3lyp-orca.freq-b3lyp.d3bj.def2svp.out
│       │   ├── 4h2o.abc0.iter1.b3lyp.smd-orca.freq-b3lyp.d3bj.def2svp.smd.out
│       ├── 4h2o.abc0.iter1-opt
│       │   ├── 4h2o.abc0.iter1-orca.opt-b3lyp.d3bj.def2svp.out
│       │   ├── 4h2o.abc0.iter1-orca.opt-b3lyp.d3bj.def2svp.smd.out
│       │   ├── 4h2o.abc0.iter1-orca.opt.r-b3lyp.d3bj.def2svp.out
│       │   ├── 4h2o.abc0.iter1-orca.opt.r-b3lyp.d3bj.def2svp.smd.out
│       └── 4h2o.abc0.iter1-sp
│           ├── 4h2o.abc0.1.b3lyp
│           │   ├── 4h2o.abc0.iter1.b3lyp-orca.sp-b3lyp.d3bj.def2tzvp.out
│           │   ├── 4h2o.abc0.iter1.b3lyp-orca.sp-wb97xd3.def2tzvp.out
│           │   └── 4h2o.abc0.iter1.b3lyp-orca.sp-wb97xd3.madef2tzvp.out
│           ├── 4h2o.abc0.1.b3lyp.smd
│           │   ├── 4h2o.abc0.iter1.b3lyp.smd-orca.sp-b3lyp.d3bj.def2tzvp.out
│           │   ├── 4h2o.abc0.iter1.b3lyp.smd-orca.sp-wb97xd3.def2tzvp.smd.out
│           │   └── 4h2o.abc0.iter1.b3lyp.smd-orca.sp-wb97xd3.madef2tzvp.smd.out
├── 4h2o.abc0.iter2
│   ├── 4h2o.abc0.iter2-calcs
│   │   └── 4h2o.abc0.iter2-opt
│   │       └── 4h2o.abc0.iter2-orca.opt-mp2.def2tzvp.out
│   └── 4h2o.abc0.iter2.mp2.xyz
```

### Abbreviations

Several abbreviations are used throughout the data set such as:

- Chemical species
    - ``h2o``: water (H<sub>2</sub>O), ``mecn``: acetonitrile (CH<sub>3</sub>CN), ``meoh``: methanol (CH<sub>3</sub>OH).
- Programs
    - ``abc``: ABCluster, ``pm``: packmol

## Contributors

Anyone who has contributed data or devoted time towards curating the data set.
Please let us know if your name should included.

- John A. Keith (Pitt)
- Alex M. Maldonado (Pitt)
- Yasemin Basdogan (Pitt)

## Citation

```text
@misc{keithgroup-solute-solvent-clusters,
  author={Alex M. Maldonado and John A. Keith},
  title={Solute-solvent clusters},
  year={2022},
  publisher={Zenodo},
  version={v2.0.0}
}
```

## License

[![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a
[Creative Commons Attribution 4.0 International License][cc-by].

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
