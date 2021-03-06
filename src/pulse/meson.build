configure_file(input : 'version.h.in', output :  'version.h', configuration : cdata)

libpulse_sources = [
  'channelmap.c',
  'context.c',
  'direction.c',
  'error.c',
  'ext-device-manager.c',
  'ext-device-restore.c',
  'ext-stream-restore.c',
  'format.c',
  'introspect.c',
  'mainloop-api.c',
  'mainloop-signal.c',
  'mainloop.c',
  'operation.c',
  'proplist.c',
  'rtclock.c',
  'sample.c',
  'scache.c',
  'stream.c',
  'subscribe.c',
  'thread-mainloop.c',
  'timeval.c',
  'utf8.c',
  'util.c',
  'volume.c',
  'xmalloc.c',
]

libpulse_headers = [
  'cdecl.h',
  'channelmap.h',
  'context.h',
  'def.h',
  'direction.h',
  'error.h',
  'ext-device-manager.h',
  'ext-device-restore.h',
  'ext-stream-restore.h',
  'format.h',
  'gccmacro.h',
  'internal.h',
  'introspect.h',
  'mainloop-api.h',
  'mainloop-signal.h',
  'mainloop.h',
  'operation.h',
  'proplist.h',
  'pulseaudio.h',
  'rtclock.h',
  'sample.h',
  'scache.h',
  'stream.h',
  'subscribe.h',
  'thread-mainloop.h',
  'timeval.h',
  'utf8.h',
  'util.h',
  'volume.h',
  'xmalloc.h',
]

if glib_dep.found()
  libpulse_headers += 'glib-mainloop.h'
endif

libpulse = shared_library('pulse',
  libpulse_sources,
  libpulse_headers,
  version : libversion,
  include_directories : [configinc, topinc],
  c_args : [pa_c_args],
  soversion : soversion,
  install : true,
  dependencies : [libm_dep, thread_dep, libpulsecommon_dep, dbus_dep],
  implicit_include_directories : false)

libpulse_dep = declare_dependency(link_with: libpulse)

if glib_dep.found()
  # TODO we must install libpulse-mainloop-glib.pc
  libpulse_mainloop_glib = shared_library('pulse-mainloop-glib',
    'glib-mainloop.c',
    'glib-mainloop.h',
    version : libpulse_mainloop_glib_version,
    c_args : [pa_c_args],
    include_directories : [configinc, topinc],
    dependencies : [libpulse_dep, libpulsecommon_dep, glib_dep],
    install : true,
  )
endif

# Configuration files

client_conf = configuration_data()
client_conf.set('PA_BINARY', cdata.get_unquoted('PA_BINARY'))

client_conf_file = configure_file(
  input : 'client.conf.in',
  output : 'client.conf',
  configuration : client_conf,
  install_dir : pulsesysconfdir,
)
