# FFTW3

![workflow](https://github.com/SciNim/nimfftw3/actions/workflows/ci.yml/badge.svg)
![workflow](https://github.com/SciNim/nimfftw3/actions/workflows/docs.yml/badge.svg)

## Introduction

Nim bindings to the FFTW3 library, to compute Fourier transforms of various kinds with high performance.

## Installation

* Install FFTW3 library
  * ex: `sudo apt-get install fftw3 fftw3-devel`
  * ex: `sudo zypper install fftw3-devel`
  * There are different FFTW3 libraries compiled with different options, the bindings should work with all of them. If it does not, open an issue and I'll look into it.
* Install the bindings `nimble install fftw3` 
To generate the documentation locally use ``nimble doc --project src/fftw3.nim --out:docs/`` or ``nimble gendoc``

Note that FFTW3 is untested for Windows but a Windows version exists. 

## Usage

### Documentations

API Documentations with some examples : https://scinim.github.io/nimfftw3/

FFTW3 official documentation : http://www.fftw.org/fftw3_doc/

### Example

See ``tests/testall.nim`` for example of FFT using Seq and Tensor.

### FFTW3 facts that will surprise you 

All this is written in the documentation and FFTW's FAQ (http://www.fftw.org/faq/section3.html) but it's not intuitive so I'll write it here. 

> Question 3.8. FFTW gives different results between runs
 If you use FFTW_MEASURE or FFTW_PATIENT mode, then the algorithm FFTW employs is not deterministic: it depends on runtime performance measurements. This will cause the results to vary slightly from run to run. However, the differences should be slight, on the order of the floating-point precision, and therefore should have no practical impact on most applications.

 If you use saved plans (wisdom) or FFTW_ESTIMATE mode, however, then the algorithm is deterministic and the results should be identical between runs.

>  Question 3.10. Why does your inverse transform return a scaled result?
Computing the forward transform followed by the backward transform (or vice versa) yields the original array scaled by the size of the array. (For multi-dimensional transforms, the size of the array is the product of the dimensions.) We could, instead, have chosen a normalization that would have returned the unscaled array. Or, to accomodate the many conventions in this matter, the transform routines could have accepted a "scale factor" parameter. We did not do this, however, for two reasons. First, we didn't want to sacrifice performance in the common case where the scale factor is 1. Second, in real applications the FFT is followed or preceded by some computation on the data, into which the scale factor can typically be absorbed at little or no cost. 

## Contributing and evolution

Any help and contribution is welcome !

As much as possible, breaking change in API should be avoided.
Improving documentation and providing better high-level API are the focus for now.

## History

These bindings were originally generated here : https://github.com/ziotom78/nimfftw3/blob/master/fftw3.nim

## License

These bindings are released under a LGPL license. FFTW3 is released under a GPLv2 or above license.
