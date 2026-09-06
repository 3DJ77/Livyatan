# Third-party licenses — structor

The `structor` binary statically links the Rust crates below (and, via `-sys` crates,
the C/C++ libraries they bundle). Each is used under the license its authors chose; for
crates offering a choice (e.g. `MIT OR Apache-2.0`), this distribution elects the MIT
license. MPL-2.0-covered crates are included unmodified; their source is available from
their crates.io and repository pages, which satisfies MPL §3.2 for this distribution.

## Fonts

The user interface embeds the Lato typeface (Łukasz Dziedzic, 2010–2014), via the fyrox
engine, under the SIL Open Font License 1.1 (https://openfontlicense.org). The font is
unmodified and is not sold separately. Full OFL text: https://spdx.org/licenses/OFL-1.1.html

## Inventory

### 0BSD OR MIT OR Apache-2.0

- adler2

### AND BSD-3-Clause

- encoding_rs

### AND Unicode-3.0

- unicode-ident

### Apache-2.0

- ab_glyph
- ab_glyph_rasterizer
- approx
- gethostname
- glutin
- glutin_egl_sys
- glutin_glx_sys
- hound
- nalgebra
- nalgebra-macros
- owned_ttf_parser
- parry2d
- parry3d
- rapier2d
- rapier3d
- simba
- winit

### Apache-2.0 / MIT

- fnv

### Apache-2.0 AND MIT

- dpi

### Apache-2.0 OR MIT

- async-channel
- async-executor
- async-io
- async-lock
- async-process
- async-signal
- async-task
- atomic-waker
- bit-vec
- blocking
- concurrent-queue
- equivalent
- event-listener
- event-listener-strategy
- fastrand
- futures-lite
- idna_adapter
- indexmap
- manifold-csg
- manifold-csg-sys
- no_std_io2
- parking
- pin-project-lite
- polling
- rustc-hash
- utf8_iter
- utf8parse
- uuid

### Apache-2.0 WITH LLVM-exception OR Apache-2.0 OR MIT

- linux-raw-sys
- rustix

### Apache-2.0/MIT

- bit_field
- fxhash

### BSD-2-Clause

- arrayref
- av1-grain
- rav1e
- v_frame

### BSD-2-Clause OR Apache-2.0 OR MIT

- zerocopy
- zerocopy-derive

### BSD-3-Clause

- avif-serialize
- exr
- instant
- lebe
- nalgebra
- ravif
- tiny-skia
- tiny-skia-path

### BSD-3-Clause OR Apache-2.0

- moxcms
- pxfm

### CC0-1.0

- notify

### CC0-1.0 OR Apache-2.0

- imgref

### ISC

- inotify
- inotify-sys
- libloading

### MIT

- aligned-vec
- alsa-sys
- arg_enum_proc_macro
- av-scenechange
- bincode
- calloop
- calloop-wayland-source
- cargo_metadata
- color_quant
- convert_case
- darling
- darling_core
- darling_macro
- ddsfile
- dlib
- drop-fyrox
- endi
- enum-primitive-derive
- equator
- equator-macro
- extended
- fax
- fyrox
- fyrox-animation
- fyrox-autotile
- fyrox-core
- fyrox-core-derive
- fyrox-graph
- fyrox-graphics
- fyrox-graphics-gl
- fyrox-impl
- fyrox-material
- fyrox-math
- fyrox-resource
- fyrox-sound
- fyrox-texture
- fyrox-ui
- glutin-winit
- hrtf
- imageproc
- inflate
- inflections
- is-docker
- is-wsl
- libm
- lightmap
- livyatan-ui
- loop9
- maybe-rayon
- memoffset
- mio
- new_debug_unreachable
- nom
- noop_proc_macro
- open
- ordered-float
- pulp
- pulp-wasm-simd-flag
- quick-xml
- raw-cpuid
- realfft
- reborrow
- rectutils
- rgb
- rubato
- sctk-adwaita
- serde-value
- simd-adler32
- simd_helpers
- slab
- smithay-client-toolkit
- smithay-clipboard
- strict-num
- strsim
- strum
- strum_macros
- synstructure
- sysinfo
- tbc
- tiff
- tinyaudio
- tracing
- tracing-attributes
- tracing-core
- uvgen
- wayland-backend
- wayland-client
- wayland-csd-frame
- wayland-cursor
- wayland-protocols
- wayland-protocols-experimental
- wayland-protocols-misc
- wayland-protocols-plasma
- wayland-protocols-wlr
- wayland-scanner
- wayland-sys
- winnow
- x11-clipboard
- x11-dl
- xcursor
- xkbcommon-dl
- y4m
- zbus
- zbus_macros
- zbus_names
- zmij
- zvariant
- zvariant_derive
- zvariant_utils

### MIT / Apache-2.0

- copypasta

### MIT OR Apache-2.0

- ahash
- aligned
- allocator-api2
- anstream
- anstyle
- anstyle-parse
- anstyle-query
- anyhow
- arrayvec
- as-raw-xcb-connection
- as-slice
- async-broadcast
- async-recursion
- async-trait
- base64
- bitflags
- bstr
- camino
- cargo-platform
- cargo-util-schemas
- cfg-if
- clap
- clap_builder
- clap_derive
- clap_lex
- colorchoice
- crc32fast
- crossbeam-deque
- crossbeam-epoch
- crossbeam-utils
- directories
- dirs-sys
- displaydoc
- document-features
- downcast-rs
- either
- ena
- enumflags2
- enumflags2_derive
- erased-serde
- errno
- fast_image_resize
- fdeflate
- flate2
- form_urlencoded
- futures
- futures-channel
- futures-core
- futures-executor
- futures-io
- futures-macro
- futures-sink
- futures-task
- futures-util
- getrandom
- gif
- glam
- glamx
- gltf
- gltf-derive
- gltf-json
- half
- hash32
- hashbrown
- heapless
- heck
- hex
- idna
- image
- image-webp
- is_terminal_polyfill
- itertools
- itoa
- jpeg-decoder
- lazy_static
- libc
- litrs
- lock_api
- log
- memmap2
- notify-types
- num
- num-bigint
- num-complex
- num-derive
- num-integer
- num-iter
- num-rational
- num-traits
- once_cell
- opener
- ordered-stream
- parking_lot
- parking_lot_core
- paste
- pastey
- percent-encoding
- piper
- png
- ppv-lite86
- primal-check
- proc-macro-crate
- proc-macro2
- profiling
- profiling-procmacros
- quote
- rand
- rand_chacha
- rand_core
- rand_distr
- rayon
- rayon-core
- regex
- regex-automata
- regex-syntax
- robust
- ron
- rstar
- rust-fuzzy-search
- rustfft
- scopeguard
- semver
- serde
- serde-untagged
- serde_core
- serde_derive
- serde_json
- serde_repr
- serde_spanned
- signal-hook-registry
- smallvec
- smol_str
- spade
- stable_deref_trait
- static_assertions
- strength_reduce
- syn
- thiserror
- thiserror-impl
- toml
- toml_datetime
- toml_edit
- toml_parser
- toml_write
- toml_writer
- transpose
- ttf-parser
- typeid
- typenum
- unicode-segmentation
- unicode-xid
- url
- weezl
- x11rb
- x11rb-protocol

### MIT OR Apache-2.0 OR Zlib

- cursor-icon
- fontdue
- glow
- raw-window-handle
- xkeysym
- zune-core
- zune-inflate
- zune-jpeg

### MIT OR Zlib OR Apache-2.0

- miniz_oxide

### MIT/Apache-2.0

- bitflags
- bitstream-io
- downcast-rs
- ident_case
- matrixmultiply
- qoi
- quick-error
- rawpointer
- scoped-tls
- vec_map

### MPL-2.0

- option-ext
- symphonia
- symphonia-bundle-flac
- symphonia-bundle-mp3
- symphonia-codec-aac
- symphonia-codec-adpcm
- symphonia-codec-alac
- symphonia-codec-pcm
- symphonia-codec-vorbis
- symphonia-core
- symphonia-format-mkv
- symphonia-format-ogg
- symphonia-format-riff
- symphonia-metadata
- symphonia-utils-xiph

### PolyForm-Small-Business-1.0.0

- bezier
- chimaera
- structor

### Unicode-3.0

- icu_collections
- icu_locale_core
- icu_normalizer
- icu_normalizer_data
- icu_properties
- icu_properties_data
- icu_provider
- litemap
- potential_utf
- tinystr
- writeable
- yoke
- yoke-derive
- zerofrom
- zerofrom-derive
- zerotrie
- zerovec
- zerovec-derive

### Unlicense OR MIT

- aho-corasick
- byteorder
- byteorder-lite
- memchr

### Unlicense/MIT

- same-file
- walkdir

### Zlib

- adler32
- foldhash

### Zlib OR Apache-2.0 OR MIT

- bytemuck
- bytemuck_derive
- safe_arch
- wide

### unspecified (see crate)

- arg_enum_proc_macro
- displaydoc
- fyrox-core-derive
- num-derive
- serde_derive
- strum_macros
- wayland-scanner
- zvariant_derive

## License texts

The full texts of the licenses referenced above are standard and unmodified; canonical
copies are at https://spdx.org/licenses/ under each identifier. Each crate's own repository
carries its copyright holders' notices verbatim.
