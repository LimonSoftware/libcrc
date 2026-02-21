project(
  'libcrc',
  'c',
   version: '2.0',
)

project_root = meson.project_source_root()
pkg = import('pkgconfig')

libcrc_inc = include_directories('include')

if get_option('build_prc')
  subdir('precalc')
else
  precalc_exe = find_program('prc')
  precalc_prog = precalc_exe.full_path()
endif
subdir('tab')

# LibCRC
if get_option('build_shared')
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
    version: meson.project_version(),
    soversion: meson.project_version().split('.')[0],
    install : true,
  )

  libcrc_dep = declare_dependency(
    link_with : libcrc_lib,
    include_directories : libcrc_inc
  )
  pkg.generate(libcrc_lib)
endif

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

if get_option('build_shared')
  libcrc32 = library('crc32',  dependencies : [libcrc32_dep])
  pkg.generate(libcrc32)
endif

# headers
install_headers(
  'include/checksum.h',
)

# tests
if get_option('build_tests')
  testall_src = [
    'test/testall.c',
    'test/testcrc.c',
    'test/testnmea.c',
  ]
  testall = executable('testall', testall_src, dependencies: libcrc_dep)
  test('testall', testall)
endif
