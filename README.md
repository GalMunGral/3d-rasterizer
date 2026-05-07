#yeaho rasterizer

## Rhetorical Design

### Purpose

For an audience familiar with real-time graphics programming but not GPU hardware, we want to communicate that rasterization — the interpolation between vertex and fragment that WebGL never exposes — is a well-defined algorithm that does not require a GPU — hardware acceleration is a performance choice, not a requirement. As in [tinyvm](https://github.com/GalMunGral/tinyvm), conformance to the specification is sufficient — Mesa3D's LLVMpipe does exactly this for the full OpenGL pipeline.

### Strategy

The project runs entirely in the browser with no GPU involvement — the same environment where WebGL operates. Only the rasterization stage is covered here; extending it to a complete software pipeline would mean interpreting shader programs per vertex and per fragment.

The interconnections make the point concrete. [svg.c](https://github.com/GalMunGral/svg.c) applies scanline rasterization to arbitrary polygons in 2D; this project reduces the primitive to the triangle and adds a depth buffer. [vector-rendering](https://github.com/GalMunGral/vector-rendering) then reframes the same problem by triangulating paths and delegating to the GPU. [raster-tile-renderer](https://github.com/GalMunGral/raster-tile-renderer) and [vector-tiles-gl](https://github.com/GalMunGral/vector-tiles-gl) are another instance of the same tradeoff, applied to web maps.
