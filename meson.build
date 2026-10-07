project('gnome-rounded-blur', 'c',
  version: '1.0.0',
  license: 'GPL-3.0-or-later',
  meson_version: '>= 0.56.0',
  default_options: [
    'warning_level=2',
    'c_std=gnu11',
  ],
)

# Project information
project_name = meson.project_name()
project_version = meson.project_version()

# API version
api_version = '1.0'

# Directories
prefix = get_option('prefix')
libdir = join_paths(prefix, get_option('libdir'))
includedir = join_paths(prefix, get_option('includedir'))
datadir = join_paths(prefix, get_option('datadir'))

mutter_req = '>= 50.0'

# The mutter API version matches the GNOME major version (e.g. 50, 51, ...)
# and bumps every release, so detect the installed one instead of hardcoding.
mutter_api_version = ''
foreach version : ['52', '51', '50']
  if dependency('libmutter-' + version, required: false).found()
    mutter_api_version = version
    break
  endif
endforeach

if mutter_api_version == ''
  error('No supported libmutter (>= 50) found')
endif

clutter_pc = 'mutter-clutter-' + mutter_api_version
cogl_pc = 'mutter-cogl-' + mutter_api_version

# Dependencies
glib_dep = dependency('glib-2.0', version: '>= 2.66')
gobject_dep = dependency('gobject-2.0', version: '>= 2.66')
clutter_dep = dependency(clutter_pc, version: mutter_req,
  required: false,
)

cogl_dep = dependency(cogl_pc, version: mutter_req,
  required: false,
)
libmutter_dep = dependency('libmutter-' + mutter_api_version)

# Required dependencies
deps = [
  glib_dep,
  gobject_dep,
  clutter_dep,
  cogl_dep,
  libmutter_dep
]

# GObject Introspection
gnome = import('gnome')
gir = find_program('g-ir-scanner', required: true)
gir_compiler = find_program('g-ir-compiler', required: true)

# Source subdirectory
subdir('src')
