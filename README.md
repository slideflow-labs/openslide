# OpenSlide

OpenSlide is a C library for reading whole slide image files (also known as
virtual slides).  It provides a consistent and simple API for reading files
from multiple vendors.

## Slideflow Labs fork

This LGPL-2.1-only fork was modified by Slideflow Labs on 2026-08-02 to
carry a narrow Leica Versa compatibility change:

- A valid, finite, positive objective below 2× identifies a low-power macro
  image when the device model is exactly `Versa`.
- A supplemental Leica label IFD is exposed as the `label` associated image.

The change preserves OpenSlide's existing canvas, offsets, main-pyramid
validation, and region bounds. It does not truncate inconsistent pyramids or
replace Leica collection dimensions with main-image dimensions.

Builds identify themselves with the version suffix `slideflow.1.0.0`. Use the
normal Meson commands below; override the suffix only when producing a newly
versioned Slideflow release:

```
meson setup builddir --buildtype=release
meson compile -C builddir
meson test -C builddir --print-errorlogs
meson install -C builddir
```

The complete source code for this fork, including its build and installation
scripts, is provided under the same LGPL-2.1-only license as OpenSlide. See
`COPYING.LESSER`.


## Features

OpenSlide can read brightfield whole slide images in [several formats][]:

* [Aperio][] (`.svs`)
* [ARGOS][] (`.avs`)
* [DICOM][] (`.dcm`)
* [Hamamatsu][] (`.ndpi`, `.vms`, `.vmu`)
* [Huron][] (`.tif`)
* [Leica][] (`.scn`)
* [MIRAX][] (`.mrxs`)
* [Philips][] (`.tiff`)
* [Sakura][] (`.svslide`)
* [Trestle][] (`.tif`)
* [Ventana][] (`.bif`, `.tif`)
* [Zeiss][] (`.czi`)
* [Generic tiled TIFF][] (`.tif`)

OpenSlide can also provide access to ICC profiles, textual metadata, and
associated images such as a slide label and thumbnail.

[several formats]: https://openslide.org/formats/
[Aperio]: https://openslide.org/formats/aperio/
[ARGOS]: https://openslide.org/formats/argos/
[DICOM]: https://openslide.org/formats/dicom/
[Hamamatsu]: https://openslide.org/formats/hamamatsu/
[Huron]: https://openslide.org/formats/huron/
[Leica]: https://openslide.org/formats/leica/
[MIRAX]: https://openslide.org/formats/mirax/
[Philips]: https://openslide.org/formats/philips/
[Sakura]: https://openslide.org/formats/sakura/
[Trestle]: https://openslide.org/formats/trestle/
[Ventana]: https://openslide.org/formats/ventana/
[Zeiss]: https://openslide.org/formats/zeiss/
[Generic tiled TIFF]: https://openslide.org/formats/generic-tiff/


## Documentation

The [API reference][API] is available on the web, and is also included as
`doc/html/openslide_8h.html` in the source tarball.  [Additional
documentation][docs] is available on the [OpenSlide website][website].

[API]: https://openslide.org/api/openslide_8h.html
[docs]: https://openslide.org/#documentation
[website]: https://openslide.org/


## License

OpenSlide is released under the terms of the [GNU Lesser General Public
License, version 2.1](https://openslide.org/license/).

OpenSlide is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for
more details.


## Compiling

To build OpenSlide, you will need:

- GCC or Clang
- Meson
- cairo ≥ 1.2
- glib ≥ 2.56
- libdicom ≥ 1.3 (automatically built if missing)
- libjpeg-turbo ≥ 1.3 or libjpeg ≥ 9c
- libpng
- libtiff ≥ 4.0
- libxml2
- OpenJPEG ≥ 2.1
- SQLite ≥ 3.14
- zlib
- Zstandard

Then:

```
meson setup builddir
meson compile -C builddir
meson install -C builddir
```


## Acknowledgements

OpenSlide has been developed by Carnegie Mellon University and other
contributors.

OpenSlide has been supported by the National Institutes of Health and
the Clinical and Translational Science Institute at the University of
Pittsburgh.

Development of DICOM and ICC functionality was supported by NCI Imaging
Data Commons and has been funded in whole or in part with Federal funds
from the National Cancer Institute, National Institutes of Health, under
Task Order No. HHSN26110071 under Contract No. HHSN261201500003l.
