# ===== Generate Currency Convert bin ===== 
configure_file(
  input: 'aria2-gui.in',
  output: 'aria2-gui',
  configuration: conf,
  install: true,
  install_dir: get_option('bindir'),
  install_mode: 'r-xr--r--'
)

## ===== Generate define module
configure_file(
  input: 'define.in',
  output: 'define.py',
  configuration: conf,
  install: true,
  install_dir: moduledir
)

# ===== Blueprint compiler =====
blueprints = custom_target('blueprints',
  input: files(
    'components/shortcuts/shortcuts.blp',
    'components/theme_selector/theme_selector.blp',
    'window.blp',
  ),
  output: '.',
  command: [find_program('blueprint-compiler'), 'batch-compile', '@OUTPUT@', '@CURRENT_SOURCE_DIR@', '@INPUT@'],
)

gnome.compile_resources('aria2-gui',
  'aria2-gui.gresource.xml',
  dependencies: blueprints,
  gresource_bundle: true,
  install: true,
  install_dir: pkgdatadir,
)

aria2_gui_sources = [
  '__init__.py',
  'components/shortcuts/shortcuts.py',
  'components/theme_selector/theme_selector.py',
  'main.py',
  'window.py',
]
install_subdir('components', install_dir: moduledir)
install_data(aria2_gui_sources, install_dir: moduledir)
