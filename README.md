# Convolver

[![Gem Version](https://badge.fury.io/rb/convolver.png)](http://badge.fury.io/rb/convolver)
[![Build Status](https://travis-ci.org/neilslater/convolver.png?branch=master)](http://travis-ci.org/neilslater/convolver)
[![Dependency Status](https://gemnasium.com/neilslater/convolver.png)](https://gemnasium.com/neilslater/convolver)

Calculates discrete convolution between two multi-dimensional arrays of floats.
See http://en.wikipedia.org/wiki/Convolution

## Installation

### Dependency: FFTW3

Before you install *convolver*, you should install the FFTW3 library on your system.
See http://www.fftw.org/ for details.

### Installing the gem

Add this line to your application's Gemfile:

    gem 'convolver'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install convolver

## Usage

Basic convolution:

    a = NArray[0.3,0.4,0.5]
    b = NArray[1.3, -0.5]
    c = Convolver.convolve( a, b )
    => NArray.float(2): [ 0.19, 0.27 ]

 * Convolver only works on single-precision floats internally. It will cast NArray types to this, if
possible, prior to calculating. For best speed, use NArray.sfloat arrays.

 * The output is smaller than the input, it only contains fully-calculated values. The output size
is the original size, minus the kernel size, plus 1, in each dimension.

 * Convolver expects input a and kernel b to have the same rank, and for the kernel to be same size
or smaller in all dimensions as the input.

 * Convolver.convolve will try to choose the faster of two approaches it has coded. In general,
small convolutions are processed directly by multiplying out all combinations and summing them,
and large convolutions are processed using FFTW3 to convert to frequency space where convolution
is simpler and faster to calculate, then convert back.

## Convolutional Neural Nets

Code for CNNs in Ruby, based on the convolve_basic method from this gem, is planned for a
new gem.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
