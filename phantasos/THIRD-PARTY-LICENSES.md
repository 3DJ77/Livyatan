# Third-party licenses — phantasos

The `phantasos` binary statically links the Rust crates below (and, via
`-sys` crates, the C/C++ libraries they bundle). Each is used under the
license its authors chose; the standard texts follow the inventory.
For crates offering a choice (e.g. `MIT OR Apache-2.0`), this
distribution elects the MIT license.

MPL-2.0 note: MPL-covered crates (the `symphonia` family, `option-ext`)
are included unmodified; their source is available from their crates.io
and repository pages, which satisfies MPL §3.2's source-availability
requirement for this distribution.

## Fonts

The user interface embeds the Lato typeface (Łukasz Dziedzic, 2010–2014), via the fyrox
engine, under the SIL Open Font License 1.1 (https://openfontlicense.org). The font is
unmodified and is not sold separately. Full OFL text: https://spdx.org/licenses/OFL-1.1.html

## Inventory

### (Apache-2.0 OR MIT) AND BSD-3-Clause

- encoding_rs 0.8.35

### (MIT OR Apache-2.0) AND NCSA

- libfuzzer-sys 0.4.13

### (MIT OR Apache-2.0) AND Unicode-3.0

- unicode-ident 1.0.24

### 0BSD OR MIT OR Apache-2.0

- adler2 2.0.1

### Apache-2.0

- ab_glyph 0.2.32
- ab_glyph_rasterizer 0.1.10
- approx 0.5.1
- clang-sys 1.9.1
- gethostname 1.1.0
- gl_generator 0.14.0
- glutin 0.32.3
- glutin_egl_sys 0.7.1
- glutin_glx_sys 0.6.1
- glutin_wgl_sys 0.6.1
- hound 3.5.1
- khronos_api 3.1.0
- nalgebra 0.34.2
- nalgebra-macros 0.3.0
- owned_ttf_parser 0.25.1
- parry2d 0.26.1
- parry3d 0.26.1
- rapier2d 0.32.0
- rapier3d 0.32.0
- simba 0.8.1
- simba 0.9.1
- winit 0.30.13

### Apache-2.0 / MIT

- fnv 1.0.7

### Apache-2.0 AND MIT

- dpi 0.1.2

### Apache-2.0 OR MIT

- async-channel 2.5.0
- async-executor 1.14.0
- async-io 2.6.0
- async-lock 3.4.2
- async-process 2.5.0
- async-signal 0.2.14
- async-task 4.7.1
- atomic-waker 1.1.2
- autocfg 1.5.1
- bit-vec 0.8.0
- blocking 1.6.2
- concurrent-queue 2.5.0
- equivalent 1.0.2
- event-listener 5.4.2
- event-listener-strategy 0.5.4
- fastrand 2.5.0
- futures-lite 2.6.1
- idna_adapter 1.2.2
- indexmap 2.14.0
- no_std_io2 0.9.4
- ntapi 0.4.3
- parking 2.2.1
- pin-project 1.1.13
- pin-project-internal 1.1.13
- pin-project-lite 0.2.17
- polling 3.11.0
- rustc-hash 2.1.3
- simd_cesu8 1.2.0
- utf8_iter 1.0.4
- utf8parse 0.2.2
- uuid 1.24.0

### Apache-2.0 WITH LLVM-exception OR Apache-2.0 OR MIT

- linux-raw-sys 0.12.1
- linux-raw-sys 0.4.15
- rustix 0.38.44
- rustix 1.1.4
- wasi 0.11.1+wasi-snapshot-preview1
- wasip2 1.0.4+wasi-0.2.12
- wit-bindgen 0.57.1

### Apache-2.0/MIT

- bit_field 0.10.3
- cexpr 0.6.0
- fxhash 0.2.1

### BSD-2-Clause

- arrayref 0.3.9
- av1-grain 0.2.5
- rav1e 0.8.1
- v_frame 0.3.9

### BSD-2-Clause OR Apache-2.0 OR MIT

- zerocopy 0.8.56
- zerocopy-derive 0.8.56

### BSD-3-Clause

- avif-serialize 0.8.9
- bindgen 0.72.1
- exr 1.74.2
- instant 0.1.13
- lebe 0.5.3
- nalgebra 0.32.6
- ravif 0.13.0
- tiny-skia 0.11.4
- tiny-skia-path 0.11.4

### BSD-3-Clause OR Apache-2.0

- moxcms 0.8.1
- pxfm 0.1.30

### BSD-3-Clause OR MIT OR Apache-2.0

- num_enum 0.7.6
- num_enum_derive 0.7.6

### BSL-1.0

- clipboard-win 5.4.1
- error-code 3.3.2

### CC0-1.0

- notify 8.2.0

### CC0-1.0 OR Apache-2.0

- imgref 1.12.2

### ISC

- inotify 0.11.4
- inotify-sys 0.1.8
- libloading 0.8.9
- libloading 0.9.0

### MIT

- aligned-vec 0.6.4
- alsa-sys 0.3.1
- android-properties 0.2.2
- arg_enum_proc_macro 0.3.4
- av-scenechange 0.14.1
- bincode 1.3.3
- block2 0.5.1
- built 0.8.1
- bytes 1.12.1
- calloop 0.13.0
- calloop 0.14.4
- calloop-wayland-source 0.3.0
- calloop-wayland-source 0.4.1
- cargo_metadata 0.22.0
- cfg_aliases 0.2.2
- color_quant 1.1.0
- combine 4.6.7
- convert_case 0.6.0
- core_maths 0.1.1
- coreaudio-sys 0.2.18
- crunchy 0.2.4
- darling 0.14.4
- darling_core 0.14.4
- darling_macro 0.14.4
- ddsfile 0.5.2
- dispatch 0.2.0
- dlib 0.5.3
- endi 1.1.1
- enum-primitive-derive 0.2.2
- equator 0.4.2
- equator-macro 0.4.2
- extended 0.1.0
- fax 0.2.7
- fsevent-sys 4.1.0
- fyrox 1.0.1
- fyrox-animation 1.0.1
- fyrox-autotile 1.0.1
- fyrox-core 1.0.1
- fyrox-core-derive 1.0.1
- fyrox-graph 1.0.1
- fyrox-graphics 1.0.1
- fyrox-graphics-gl 1.0.1
- fyrox-impl 1.0.1
- fyrox-material 1.0.1
- fyrox-math 1.0.1
- fyrox-resource 1.0.1
- fyrox-sound 1.0.1
- fyrox-texture 1.0.1
- fyrox-ui 1.0.1
- glutin-winit 0.5.0
- hrtf 0.8.1
- imageproc 0.25.1
- inflate 0.4.5
- inflections 1.1.1
- interpolate_name 0.2.4
- is-docker 0.2.0
- is-wsl 0.4.0
- kqueue 1.2.1
- kqueue-sys 1.1.2
- libm 0.2.16
- libredox 0.1.19
- lightmap 0.6.0
- loop9 0.1.5
- maybe-rayon 0.1.1
- memoffset 0.9.1
- mio 1.2.2
- new_debug_unreachable 1.0.6
- nom 7.1.3
- nom 8.0.0
- noop_proc_macro 0.3.0
- objc-sys 0.3.5
- objc2 0.5.2
- objc2 0.6.4
- objc2-app-kit 0.2.2
- objc2-cloud-kit 0.2.2
- objc2-contacts 0.2.2
- objc2-core-data 0.2.2
- objc2-core-image 0.2.2
- objc2-core-location 0.2.2
- objc2-encode 4.1.0
- objc2-foundation 0.2.2
- objc2-foundation 0.3.2
- objc2-link-presentation 0.2.2
- objc2-metal 0.2.2
- objc2-quartz-core 0.2.2
- objc2-symbols 0.2.2
- objc2-ui-kit 0.2.2
- objc2-uniform-type-identifiers 0.2.2
- objc2-user-notifications 0.2.2
- open 5.4.1
- orbclient 0.3.55
- ordered-float 2.10.1
- ordered-float 5.3.0
- pulp 0.22.3
- pulp-wasm-simd-flag 0.1.1
- quick-xml 0.41.0
- raw-cpuid 11.6.0
- realfft 3.5.0
- reborrow 0.5.5
- rectutils 0.5.0
- redox_syscall 0.4.1
- redox_syscall 0.5.18
- redox_syscall 0.9.1
- redox_users 0.4.6
- rgb 0.8.53
- rubato 0.14.1
- sctk-adwaita 0.10.1
- serde-value 0.7.0
- serde-wasm-bindgen 0.6.5
- simd-adler32 0.3.10
- simd_helpers 0.1.0
- slab 0.4.12
- smithay-client-toolkit 0.19.2
- smithay-client-toolkit 0.20.0
- smithay-clipboard 0.7.3
- strict-num 0.1.1
- strsim 0.10.0
- strsim 0.11.1
- strum 0.27.2
- strum_macros 0.27.2
- synstructure 0.13.2
- sysinfo 0.29.11
- tbc 0.3.0
- tiff 0.11.3
- tinyaudio 2.0.0
- tracing 0.1.44
- tracing-attributes 0.1.31
- tracing-core 0.1.36
- uds_windows 1.2.1
- uvgen 0.3.0
- wayland-backend 0.3.16
- wayland-client 0.31.15
- wayland-csd-frame 0.3.0
- wayland-cursor 0.31.14
- wayland-protocols 0.32.13
- wayland-protocols-experimental 20250721.0.1
- wayland-protocols-misc 0.3.12
- wayland-protocols-plasma 0.3.12
- wayland-protocols-wlr 0.3.12
- wayland-scanner 0.31.11
- wayland-sys 0.31.11
- winnow 0.7.15
- winnow 1.0.4
- x11-clipboard 0.9.3
- x11-dl 2.21.0
- xcursor 0.3.11
- xkbcommon-dl 0.4.2
- xml-rs 0.8.29
- y4m 0.8.0
- zbus 5.19.0
- zbus_macros 5.19.0
- zbus_names 4.3.4
- zcheapstr 1.1.0
- zmij 1.0.23
- zvariant 5.14.0
- zvariant_derive 5.14.0
- zvariant_utils 4.0.0

### MIT / Apache-2.0

- cgl 0.3.2
- copypasta 0.10.2

### MIT OR Apache-2.0

- ahash 0.8.12
- aligned 0.4.3
- allocator-api2 0.2.21
- android-activity 0.6.1
- anstream 1.0.0
- anstyle 1.0.14
- anstyle-parse 1.0.0
- anstyle-query 1.1.5
- anstyle-wincon 3.0.11
- anyhow 1.0.104
- arbitrary 1.4.2
- arrayvec 0.7.8
- as-raw-xcb-connection 1.0.1
- as-slice 0.2.1
- async-broadcast 0.7.2
- async-recursion 1.1.1
- async-trait 0.1.92
- base64 0.22.1
- bitflags 2.13.1
- bstr 1.13.1
- bumpalo 3.20.3
- camino 1.2.5
- cargo-platform 0.3.3
- cargo-util-schemas 0.8.2
- cc 1.4.2
- cfg-if 1.0.4
- clap 4.6.6
- clap_builder 4.6.6
- clap_derive 4.6.4
- clap_lex 1.1.0
- colorchoice 1.0.5
- core-foundation 0.9.4
- core-foundation-sys 0.8.7
- core-graphics 0.23.2
- core-graphics-types 0.1.3
- crc32fast 1.5.0
- crossbeam-deque 0.8.7
- crossbeam-epoch 0.9.20
- crossbeam-utils 0.8.22
- directories 5.0.1
- dirs-sys 0.4.1
- displaydoc 0.2.7
- document-features 0.2.12
- downcast-rs 2.0.2
- either 1.17.0
- ena 0.14.4
- enumflags2 0.7.12
- enumflags2_derive 0.7.12
- erased-serde 0.4.10
- errno 0.3.14
- fast_image_resize 5.5.0
- fdeflate 0.3.7
- find-msvc-tools 0.1.10
- flate2 1.1.9
- form_urlencoded 1.2.2
- futures 0.3.33
- futures-channel 0.3.33
- futures-core 0.3.33
- futures-executor 0.3.33
- futures-io 0.3.33
- futures-macro 0.3.33
- futures-sink 0.3.33
- futures-task 0.3.33
- futures-util 0.3.33
- getrandom 0.2.17
- getrandom 0.3.4
- getrandom 0.4.3
- gif 0.14.2
- glam 0.14.0
- glam 0.15.2
- glam 0.16.0
- glam 0.17.3
- glam 0.18.0
- glam 0.19.0
- glam 0.20.5
- glam 0.21.3
- glam 0.22.0
- glam 0.23.0
- glam 0.24.2
- glam 0.25.0
- glam 0.27.0
- glam 0.28.0
- glam 0.29.3
- glam 0.30.10
- glam 0.31.1
- glam 0.32.1
- glamx 0.1.3
- glob 0.3.4
- gltf 1.4.1
- gltf-derive 1.4.1
- gltf-json 1.4.1
- half 2.7.1
- hash32 0.3.1
- hashbrown 0.15.5
- hashbrown 0.16.1
- hashbrown 0.17.1
- heapless 0.8.0
- heck 0.5.0
- hermit-abi 0.5.2
- hex 0.4.3
- idna 1.1.0
- image 0.24.9
- image 0.25.10
- image-webp 0.2.4
- is_terminal_polyfill 1.70.2
- itertools 0.12.1
- itertools 0.13.0
- itertools 0.14.0
- itoa 1.0.18
- jni 0.22.4
- jni-macros 0.22.4
- jni-sys 0.3.1
- jni-sys 0.4.1
- jni-sys-macros 0.4.1
- jobserver 0.1.35
- jpeg-decoder 0.3.2
- js-sys 0.3.104
- lazy_static 1.5.0
- libc 0.2.189
- litrs 1.0.0
- lock_api 0.4.14
- log 0.4.33
- memmap2 0.9.11
- ndk 0.9.0
- ndk-context 0.1.1
- ndk-sys 0.6.0+11769913
- normpath 1.5.1
- notify-types 2.1.0
- num 0.4.3
- num-bigint 0.4.8
- num-complex 0.4.6
- num-derive 0.4.2
- num-integer 0.1.46
- num-iter 0.1.46
- num-rational 0.4.2
- num-traits 0.2.19
- once_cell 1.21.4
- once_cell_polyfill 1.70.2
- opener 0.8.5
- ordered-stream 0.2.0
- parking_lot 0.12.5
- parking_lot_core 0.9.12
- paste 1.0.15
- pastey 0.1.1
- percent-encoding 2.3.2
- piper 0.2.5
- pkg-config 0.3.33
- png 0.17.16
- png 0.18.1
- ppv-lite86 0.2.21
- primal-check 0.3.4
- proc-macro-crate 3.5.0
- proc-macro2 1.0.107
- profiling 1.0.18
- profiling-procmacros 1.0.18
- quote 1.0.47
- rand 0.8.7
- rand 0.9.5
- rand_chacha 0.3.1
- rand_chacha 0.9.0
- rand_core 0.6.4
- rand_core 0.9.5
- rand_distr 0.4.3
- rayon 1.12.0
- rayon-core 1.13.0
- regex 1.13.1
- regex-automata 0.4.18
- regex-syntax 0.8.11
- robust 1.2.0
- ron 0.11.0
- rstar 0.12.2
- rust-fuzzy-search 0.1.1
- rustc_version 0.4.1
- rustfft 6.4.1
- rustversion 1.0.23
- scopeguard 1.2.0
- semver 1.0.28
- serde 1.0.229
- serde-untagged 0.1.9
- serde_core 1.0.229
- serde_derive 1.0.229
- serde_json 1.0.151
- serde_repr 0.1.21
- serde_spanned 0.6.9
- serde_spanned 1.1.1
- shlex 1.3.0
- shlex 2.0.1
- signal-hook-registry 1.4.8
- simdutf8 0.1.5
- smallvec 1.15.2
- smol_str 0.2.2
- spade 2.15.1
- stable_deref_trait 1.2.1
- static_assertions 1.1.0
- strength_reduce 0.2.4
- syn 1.0.109
- syn 2.0.119
- syn 3.0.3
- tempfile 3.27.0
- thiserror 1.0.69
- thiserror 2.0.20
- thiserror-impl 1.0.69
- thiserror-impl 2.0.20
- toml 0.8.23
- toml 0.9.12+spec-1.1.0
- toml_datetime 0.6.11
- toml_datetime 0.7.5+spec-1.1.0
- toml_datetime 1.1.1+spec-1.1.0
- toml_edit 0.22.27
- toml_edit 0.23.10+spec-1.0.0
- toml_edit 0.25.13+spec-1.1.0
- toml_parser 1.1.3+spec-1.1.0
- toml_write 0.1.2
- toml_writer 1.1.2+spec-1.1.0
- transpose 0.2.3
- ttf-parser 0.25.1
- typeid 1.0.3
- typenum 1.20.1
- unicode-segmentation 1.13.3
- unicode-xid 0.2.6
- url 2.5.8
- wasm-bindgen 0.2.127
- wasm-bindgen-futures 0.4.77
- wasm-bindgen-macro 0.2.127
- wasm-bindgen-macro-support 0.2.127
- wasm-bindgen-shared 0.2.127
- web-sys 0.3.104
- web-time 1.1.0
- weezl 0.1.12
- windows-link 0.2.1
- windows-sys 0.48.0
- windows-sys 0.52.0
- windows-sys 0.59.0
- windows-sys 0.60.2
- windows-sys 0.61.2
- windows-targets 0.48.5
- windows-targets 0.52.6
- windows-targets 0.53.5
- windows_aarch64_gnullvm 0.48.5
- windows_aarch64_gnullvm 0.52.6
- windows_aarch64_gnullvm 0.53.1
- windows_aarch64_msvc 0.48.5
- windows_aarch64_msvc 0.52.6
- windows_aarch64_msvc 0.53.1
- windows_i686_gnu 0.48.5
- windows_i686_gnu 0.52.6
- windows_i686_gnu 0.53.1
- windows_i686_gnullvm 0.52.6
- windows_i686_gnullvm 0.53.1
- windows_i686_msvc 0.48.5
- windows_i686_msvc 0.52.6
- windows_i686_msvc 0.53.1
- windows_x86_64_gnu 0.48.5
- windows_x86_64_gnu 0.52.6
- windows_x86_64_gnu 0.53.1
- windows_x86_64_gnullvm 0.48.5
- windows_x86_64_gnullvm 0.52.6
- windows_x86_64_gnullvm 0.53.1
- windows_x86_64_msvc 0.48.5
- windows_x86_64_msvc 0.52.6
- windows_x86_64_msvc 0.53.1
- x11rb 0.13.2
- x11rb-protocol 0.13.2

### MIT OR Apache-2.0 OR LGPL-2.1-or-later

- r-efi 5.3.0
- r-efi 6.0.0

### MIT OR Apache-2.0 OR Zlib

- cursor-icon 1.2.0
- fontdue 0.9.4
- glow 0.17.0
- raw-window-handle 0.6.2
- xkeysym 0.2.1
- zune-core 0.5.3
- zune-inflate 0.2.54
- zune-jpeg 0.5.15

### MIT OR Zlib OR Apache-2.0

- miniz_oxide 0.8.9

### MIT/Apache-2.0

- bitflags 1.3.2
- bitstream-io 4.10.0
- downcast-rs 1.2.1
- foreign-types 0.5.0
- foreign-types-macros 0.2.4
- foreign-types-shared 0.3.1
- ident_case 1.0.1
- matrixmultiply 0.3.11
- minimal-lexical 0.2.1
- plain 0.2.3
- qoi 0.4.1
- quick-error 2.0.1
- rawpointer 0.2.1
- scoped-tls 1.0.1
- vec_map 0.8.2
- version_check 0.9.5
- winapi 0.3.9
- winapi-i686-pc-windows-gnu 0.4.0
- winapi-x86_64-pc-windows-gnu 0.4.0

### MPL-2.0

- option-ext 0.2.0
- symphonia 0.5.5
- symphonia-bundle-flac 0.5.5
- symphonia-bundle-mp3 0.5.5
- symphonia-codec-aac 0.5.5
- symphonia-codec-adpcm 0.5.5
- symphonia-codec-alac 0.5.5
- symphonia-codec-pcm 0.5.5
- symphonia-codec-vorbis 0.5.5
- symphonia-core 0.5.5
- symphonia-format-mkv 0.5.5
- symphonia-format-ogg 0.5.5
- symphonia-format-riff 0.5.5
- symphonia-metadata 0.5.5
- symphonia-utils-xiph 0.5.5

### Unicode-3.0

- icu_collections 2.2.0
- icu_locale_core 2.2.0
- icu_normalizer 2.2.0
- icu_normalizer_data 2.2.0
- icu_properties 2.2.0
- icu_properties_data 2.2.0
- icu_provider 2.2.0
- litemap 0.8.2
- potential_utf 0.1.5
- tinystr 0.8.3
- writeable 0.6.3
- yoke 0.8.3
- yoke-derive 0.8.2
- zerofrom 0.1.8
- zerofrom-derive 0.1.7
- zerotrie 0.2.4
- zerovec 0.11.6
- zerovec-derive 0.11.3

### Unlicense OR MIT

- aho-corasick 1.1.5
- byteorder 1.5.0
- byteorder-lite 0.1.0
- memchr 2.8.3
- winapi-util 0.1.11

### Unlicense/MIT

- same-file 1.0.6
- walkdir 2.5.0

### Zlib

- adler32 1.2.0
- foldhash 0.1.5
- foldhash 0.2.0
- slotmap 1.1.1

### Zlib OR Apache-2.0 OR MIT

- bytemuck 1.25.2
- bytemuck_derive 1.12.0
- dispatch2 0.3.1
- objc2-app-kit 0.3.2
- objc2-core-foundation 0.3.2
- safe_arch 0.7.4
- wide 0.7.33

## License texts

The full texts of the licenses referenced above (MIT, Apache-2.0,
BSD-2-Clause, BSD-3-Clause, BSL-1.0, ISC, Zlib, CC0-1.0, Unicode-3.0,
NCSA, MPL-2.0) are standard and unmodified; canonical copies are at
https://spdx.org/licenses/ under each identifier. Each crate's own
repository carries its copyright holders' notices verbatim.
