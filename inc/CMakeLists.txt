# Distributed under the original FontForge BSD 3-clause license


set(INC_NOINST_HEADERS
  basics.h
  carbon.h
  chardata.h
  charset.h
  dlist.h
  ffgdk.h
  ffglib.h
  ../build/inc/fontforge-config.h
  ../build/inc/fontforge-version-extras.h
  gdraw.h
  gfile.h
  ggadget.h
  gicons.h
  gimage.h
  gio.h
  gkeysym.h
  gprogress.h
  gresedit.h
  gresource.h
  gutils.h
  gwidget.h
  gwwiconv.h
  hotkeys.h
  intl.h
  prefs.h
  unicodelibinfo.h
  ustring.h
  utype.h
)

add_library(fontforge_common_headers INTERFACE)

include(FontForgeConfigure)
fontforge_generate_config(fontforge-config.h.in fontforge-config.h)
fontforge_generate_version_extras(fontforge-version-extras.h.in fontforge-version-extras.h)

target_include_directories(fontforge_common_headers
  INTERFACE
    "${CMAKE_CURRENT_SOURCE_DIR}"
    "${CMAKE_CURRENT_BINARY_DIR}"
)

target_link_libraries(fontforge_common_headers
  INTERFACE
    GLIB::GLIB
)
if(ENABLE_CODE_COVERAGE_RESULT)
target_link_libraries(fontforge_common_headers
  INTERFACE
    Gcov::Gcov
)
endif()
install(FILES ${INC_NOINST_HEADERS} DESTINATION /usr/local/include/fontforge)
