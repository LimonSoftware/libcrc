project(
  'libcrc',
  'c',
   version: '2.0',
)

project_root = meson.project_source_root()

libcrc_inc = include_directories('include')

subdir('precalc')
subdir('tab')

# LibCRC
libcrc_src = [ 
  'src/crc8.c',
  'src/crc16.c',
  'src/crc32.c',
  'src/crc64.c',
  'src/crcccitt.c',
  'src/crcdnp.c',
  'src/crckrmit.c',
  'src/crcsick.c',
  'src/nmea-chk.c',
]

libcrc_lib = shared_library('crc',
  libcrc_src,
  include_directories : [libcrc_inc],
  dependencies : [gentab32_dep, gentab64_dep],
  install : true
)

libcrc_dep = declare_dependency(
  link_with : libcrc_lib,
  include_directories : libcrc_inc
)

# LibCRC32
libcrc32_lib = static_library('crc32',
  'src/crc32.c',
  include_directories : [libcrc_inc],
  dependencies : [gentab32_dep],
  install : true
)

libcrc32_dep = declare_dependency(
  link_with : libcrc32_lib,
  include_directories : libcrc_inc
)

# headers and pkg-config
install_headers(
  'include/checksum.h',
)
pkg = import('pkgconfig')
pkg.generate(libcrc_lib)
libcrc32 = library('crc32',  dependencies : [libcrc32_dep])
pkg.generate(libcrc32)

# tests
testall_src = [
  'test/testall.c',
  'test/testcrc.c',
  'test/testnmea.c',
]
testall = executable('testall', testall_src, dependencies: libcrc_dep)
test('testall', testall)
