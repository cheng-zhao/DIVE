# DIVE

![GitHub](https://img.shields.io/github/license/cheng-zhao/DIVE.svg)
![Codacy grade](https://img.shields.io/codacy/grade/b6739a329c4d4e01869ec3c7ea774953.svg)

## Table of Contents

-   [Introduction](#introduction)
-   [Compilation](#compilation)
-   [Running](#running)
-   [References](#references)

## Introduction

**D**elaunay tr**I**angulation **V**oid find**E**r (DIVE) is a tool for identifying all empty spheres that are constrained by four elements of a point set, using the Delaunay Triangulation (DT) technique. In the cosmological context, it is able to resolved all the largest spheres that are empty of tracers, such as galaxies, in either a real survey volume, or a periodic simulation box. These spheres are regarded as a special type of cosmic voids &mdash; DT voids &mdash; which are allowed to overlap with each other.

The size of DT voids statistically represents the density of the dark matter field in the Universe<sup>[\[1\]](#ref1)</sup>. Using the large DT voids, it has been reported for the first time the baryon acoustic oscillation (BAO) signature from under-densities of the Universe<sup>[\[2\]](#ref2)[\[3\]](#ref3)</sup>. This feature is found to encode additional cosmological information, compared to the clustering of galaxies. By combining measurements from galaxies and DT voids, we are able to achieve better cosmological parameter constraints<sup>[\[4\]](#ref4)</sup>. Thus, DIVE is potentially a powerful tool for cosmological studies.

This program is compliant with the C++11 standard, and relies largely on the [Computational Geometry Algorithms Library](https://www.cgal.org/) (CGAL). It is written by Cheng Zhao (&#36213;&#25104;), and is distributed under the [GPLv3 license](LICENSE.txt).

If you use this tool in research work that results in publications, please cite the following paper:

> Zhao et al., 2016, [DIVE in the cosmic web: voids with Delaunay triangulation from discrete matter tracer distributions](https://doi.org/10.1093/mnras/stw660), *MNRAS*, 459(3):2670&ndash;2680 ([arXiv:1511.04299](https://arxiv.org/abs/1511.04299))

## Compilation

To build DIVE, the CGAL library and its dependencies has to be previously downloaded or installed, including (see also the [CGAL manual](https://doc.cgal.org/latest/Manual/thirdparty.html) for details)

-   [CMake](https://cmake.org/)
-   [GNU Multiple Precision Arithmetic Library](https://gmplib.org/) (GMP)
-   [GNU Multiple Precision Floating-Point Reliably Library](https://www.mpfr.org/) (MPFR)
-   [Boost library](https://www.boost.org/)
-   [CGAL](https://www.cgal.org/)

Please consult the documentations of these dependences for the installations. The good news is that recent versions of Boost and CGAL can be used in a "header-only" way, that is to say, it is not necessary to build them.

Once the prerequisites are ready, DIVE can be compiled in the following way:

```bash
cd /path/with/DIVE.cpp/
/path/to/CGAL/Scripts/scripts/cgal_create_CMakeLists
cmake -DCMAKE_BUILD_TYPE=Release -DCGAL_DIR=/path/to/CGAL -DBOOST_ROOT=/path/to/Boost -DCMAKE_CXX_COMPILER=g++ -DCMAKE_C_COMPILER=gcc
make
```

Here, some of the commonly used flags for `cmake` are shown, but they are not always necessary. A comprehensive list of CMake options for DIVE can be found in the [CGAL manual](https://doc.cgal.org/latest/Manual/configurationvariables.html).

## Running

The `DIVE` executable should be run with command line options that specify the input and output catalogues. Optionally, the boundaries for periodic conditions can be passed via command line as well. A list of supported options is shown below

| Option | Mandatory | Description                                             |
|:------:|:---------:|---------------------------------------------------------|
| `-h`   | &cross;   | Display the list of command line options                |
| `-i`   | &check;   | Specify the input tracer catalogue                      |
| `-o`   | &check;   | Specify the output DT void catalogue                    |
| `-l`   | &cross;   | Set the lower boundary of the periodic box (default: 0) |
| `-u`   | &cross;   | Set the upper boundary of the periodic box              |

Here, the first 3 columns of the input catalogues must be the 3D coordinates of tracers, which are typically in comoving space. The resulting void catalogue contains 4 columns: {*x*<sub>c</sub> , *y*<sub>c</sub> , *z*<sub>c</sub> , *R*<sub>v</sub>}, i.e., coordinates of the void centres, as well as the radii.

If the upper boundary (*B*<sub>max</sub>) of the periodic box is supplied, the Delaunay Triangulation will be constructed with periodic boundary conditions. In particular, the lower boundary of the box (*B*<sub>min</sub>) is set to 0, if it is not provided specifically. Coordinates of tracers in the periodic box, should be no smaller than the *B*<sub>min</sub>, but less than *B*<sub>max</sub>.

## References

<span id="ref1">\[1\]</span> Zhao, Tao, Liang, Kitaura, Chuang, 2016, [DIVE in the cosmic web: voids with Delaunay triangulation from discrete matter tracer distributions](https://doi.org/10.1093/mnras/stw660), *MNRAS*, 459(3):2670&ndash;2680 ([arXiv:1511.04299](https://arxiv.org/abs/1511.04299))

<span id="ref2">\[2\]</span> Liang, Zhao, Chuang, Kitaura, Tao, 2016, [Measuring baryon acoustic oscillations from the clustering of voids](https://doi.org/10.1093/mnras/stw884), *MNRAS*, 459(4):4020&ndash;4028 ([arXiv:1511.04391](https://arxiv.org/abs/1511.04391))

<span id="ref3">\[3\]</span> Kitaura et al., 2016, [Signatures of the Primordial Universe from Its Emptiness: Measurement of Baryon Acoustic Oscillations from Minima of the Density Field](https://doi.org/10.1103/PhysRevLett.116.171301), *Phys.Rev.Lett.*, 116, 171301 ([arXiv:1511.04405](https://arxiv.org/abs/1511.04405))

<span id="ref4">\[4\]</span> Zhao et al., 2020, [Improving baryon acoustic oscillation measurement with the combination of cosmic voids and galaxies](https://doi.org/10.1093/mnras/stz3339), *MNRAS*, 491(3):4554&ndash;4572 ([arXiv:1802.03990](https://arxiv.org/abs/1802.03990))
