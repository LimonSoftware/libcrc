# Generators
gentab32 = 'gentab32'
gentab32_output = gentab32 + '.inc'
gentab32_inc = custom_target(
  gentab32,
  output: gentab32_output,
  command: [precalc_prog, '--crc32', '@OUTPUT@'],
  depends: [precalc_prog],
  build_by_default: true,
)
gentab32_dep = declare_dependency(
  sources: gentab32_inc,
  include_directories : '.',
)

gentab64 = 'gentab64'
gentab64_output = gentab64 + '.inc'
gentab64_inc = custom_target(
  gentab64,
  output: gentab64_output,
  command: [precalc_prog, '--crc64', '@OUTPUT@'],
  depends: [precalc_prog],
  build_by_default: true,
)
gentab64_dep = declare_dependency(
  sources: gentab64_inc,
  include_directories : '.',
)
