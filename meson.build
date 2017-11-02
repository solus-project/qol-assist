project(
    'qol-assist',
    ['c'],
    version: '0',
    license: [
        'GPL-2.0',
    ],
    default_options: [
        'c_std=c11',
        'prefix=/usr',
        'sysconfdir=/etc',
    ],
)

am_cflags = [
    '-fstack-protector',
    '-Wall',
    '-pedantic',
    '-Wstrict-prototypes',
    '-Wundef',
    '-fno-common',
    '-Werror-implicit-function-declaration',
    '-Wformat',
    '-Wformat-security',
    '-Werror=format-security',
    '-Wconversion',
    '-Wunused-variable',
    '-Wunreachable-code',
    '-W',
    '-D_FORTIFY_SOURCE=2',
]

# Add our main flags
add_global_arguments(am_cflags, language: 'c')

# Get configuration bits together
path_prefix = get_option('prefix')
path_sysconfdir = join_paths(path_prefix, get_option('sysconfdir'))
path_datadir = join_paths(path_prefix, get_option('datadir'))
path_bindir = join_paths(path_prefix, get_option('bindir'))

# Sort out config.h now
cdata = configuration_data()

# General options..
cdata.set_quoted('PACKAGE_VERSION', meson.project_version())
cdata.set_quoted('PACKAGE_URL', 'https://solus-project.com')

# Write config.h now
config_h = configure_file(
     configuration: cdata,
     output: 'config.h',
)
config_h_dir = include_directories('.')

# Now go build the source
subdir('src')

report = [
    '    Build configuration:',
    '    ====================',
    '',
    '    prefix:                                 @0@'.format(path_prefix),
    '    datadir:                                @0@'.format(path_datadir),
    '    sysconfdir:                             @0@'.format(path_sysconfdir),
    '    bindir:                                 @0@'.format(path_bindir),
]

# Output some stuff to validate the build config
message('\n\n\n' + '\n'.join(report) + '\n\n')