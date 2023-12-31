project('aria2-gui',
  version: '0.1.0',
  meson_version: '>= 0.62.0',
  default_options: [ 'warning_level=2', 'werror=false', ],
)

i18n = import('i18n')
gnome = import('gnome')
python = import('python')

base_id = 'io.github.idevecore.Aria2GUI'
pkgdatadir = join_paths(get_option('prefix'), get_option('datadir'), meson.project_name())
moduledir = join_paths(pkgdatadir, 'aria2_gui')

if get_option('profile') == 'development'
  profile = 'Devel'
  vcs_tag = run_command('git', 'rev-parse', '--short', 'HEAD').stdout().strip()
  if vcs_tag == ''
    version_suffix = '-devel'
  else
    version_suffix = '-@0@'.format(vcs_tag)
  endif
  application_id = '@0@.@1@'.format(base_id, profile)
else
  profile = ''
  version_suffix = ''
  application_id = base_id
endif

conf = configuration_data()
conf.set('PYTHON', python.find_installation('python3').full_path())
conf.set('PROFILE', profile)
conf.set('VERSION', meson.project_version() + version_suffix)
conf.set('APP_ID', application_id)
conf.set('BIN', join_paths(get_option('prefix'), get_option('bindir'), meson.project_name()))
conf.set('pkgdatadir', pkgdatadir)
conf.set('datadir', get_option('datadir'))
conf.set('prefix', get_option('prefix'))
conf.set('localedir', join_paths(get_option('prefix'), get_option('localedir')))
subdir('data')
subdir('src')
subdir('po')

gnome.post_install(
  glib_compile_schemas: true,
  gtk_update_icon_cache: true,
  update_desktop_database: true,
)
