# squish #

## News ##

We've moved!  So far there have been just a few minor edits since version 1.10, check the [issues](http://code.google.com/p/libsquish/issues/list) for the planned changes.

Update: squish 1.11 is available, which is exactly the same as squish 1.10 but has contributed project files for vs8 and vs9.  All other changes have been deferred to 1.12.

## Features ##

The squish library (abbreviated to libsquish) is an open source DXT compression library written in C++ with the following features:

  * Supports the DXT1, DXT3 and DXT5 formats.
  * Optimised for both SSE and Altivec SIMD instruction sets.
  * Builds on multiple platforms (x86 and PPC tested).
  * Very simple interface.

A description of the algorithms used to perform the compression can be found on [my blog](http://www.sjbrown.co.uk/2006/01/19/dxt-compression-techniques/).

Note that the cluster fit algorithm in squish now forms the core DXT compression algorithm for the [NVIDIA Texture Tools](http://developer.nvidia.com/object/texture_tools.html). NVIDIA have been kind enough to allow implementation improvements to be refactored back into the library.

## Example Usage ##

See squish.h in the distribution for the documentation. The library has only two functions, one to compress a block of 4x4 pixels and one to decompress. The following program will compress then decompress a single 4x4 DXT block:

```
#include <squish.h>

int main()
{
    squish::u8 pixels[16*4];  // 16 pixels of input
    squish::u8 block[8];      // 8 bytes of output

    /* write some pixel data */

    // compress the 4x4 block using DXT1 compression
    squish::Compress( pixels, block, squish::kDxt1 );
    
    // decompress the 4x4 block using DXT1 compression
    squish::Decompress( pixels, block, squish::kDxt1 );
}
```

A wrapper API is also included to compress entire images in a single call. In addition, there is an example program provided with the library that shows how to use the squish library to compress and decompress between PNG and DXT format images.

## Contributors ##

The squish library was originally written by:
  * [Simon Brown](http://www.sjbrown.co.uk/)

The following people have made significant contributions to the squish library:
  * Ignacio Castaño (NVIDIA)

## Alternatives ##

It turns out that there are other open source DXT compression implementations out there on the interweb. Here is a list of the currently known competition:

  * Jason Dorie's image library: [ImageLib](http://www.jasondorie.com/ImageLib.zip)
  * Mesa S3TC compression library: [libtxc\_dxtn](http://homepage.hispeed.ch/rscheidegger/dri_experimental/s3tc_index.html)

I haven't had the time yet to do any comparisons between these libraries and squish. If anyone has then please let me know!