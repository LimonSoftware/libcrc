# Precalc tool
libcrc_precalc_inc = [include_directories('.'),  libcrc_inc]
libcrc_precalc_lib = static_library('precalccrc',
  'crc32_table.c',
  'crc64_table.c',
  include_directories : libcrc_precalc_inc
)

libcrc_precalc_dep = declare_dependency(
  link_with : libcrc_precalc_lib,
  include_directories : libcrc_precalc_inc
)

precalc_prog = executable('prc', 'precalc.c', dependencies: libcrc_precalc_dep, install: true)
precalc_exe = precalc_prog.full_path()
