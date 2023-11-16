# Arduino Ogg Vorbis 'Tremor' integer playback codec

Currently, the source implements playback in pure C on all platforms
except ARM, where a [currently] small amount of assembly (see
asm_arm.h) is used to implement 64 bit math operations and fast LSP
computation.  If building on ARM without the benefit of GNU build
system tools, be sure that '_ARM_ASSEM_' is #defined by the build
system if this assembly is desired, else the resulting library will
use whatever 64 bit math builtins the compiler implements.

No math library is required by this source.  No floating point
operations are used at any point in either setup or decode.  This
decoder library will properly decode any past, current or future
Vorbis I file or stream.

Further information can be found in the [original README](/README).

### Dependencies

This decoder is dependend on LibOgg, which is part of [arduino-libopus](https://github.com/pschatzmann/arduino-libopus)

### Installation in Arduino

You can download the library as zip and call include Library -> zip library. Or you can git clone this project into the Arduino libraries folder e.g. with

```
cd  ~/Documents/Arduino/libraries
git clone https://github.com/pschatzmann/arduino-libvorbis-idec.git
git clone https://github.com/pschatzmann/arduino-arduino-libopus.git
```

I recommend to use git because you can easily update to the latest version just by executing the ```git pull``` command in the project folder.

### Documentation

Detailed Tremor API Documentation can be found at [doc/index.html](https://pschatzmann.github.io/arduino-libvorbis-idec/doc/index.html)

I recommend to use this library together with my [Arduino Audio Tools](https://github.com/pschatzmann/arduino-audio-tools). 
This is just one of many __codecs__ that I have collected so far: Further details can be found in the [Encoding and Decoding Wiki](https://github.com/pschatzmann/arduino-audio-tools/wiki/Encoding-and-Decoding-of-Audio) of the Audio Tools.

### Original Source Code

The original source code can be found at https://gitlab.xiph.org/xiph/tremor
