set(QtSystemd_HEADERS
    generic-types.h
    job.h
    ldmanager.h
    sdmanager.h
    seat.h
    session.h
    unit.h
    user.h
    QtSystemd-export.h
)

set(QtSystemd_PART_SRCS
    generic-types.cpp
    job.cpp
    ldmanager.cpp
    sdmanager.cpp
    seat.cpp
    session.cpp
    unit.cpp
    user.cpp
)

set(INTERFACE_INTROSPECTION_XML_FILES
    dbus/org.freedesktop.login1.LDManager.xml
    dbus/org.freedesktop.login1.Seat.xml
    dbus/org.freedesktop.login1.Session.xml
    dbus/org.freedesktop.login1.User.xml
    dbus/org.freedesktop.systemd1.Automount.xml
    dbus/org.freedesktop.systemd1.Device.xml
    dbus/org.freedesktop.systemd1.Job.xml
    dbus/org.freedesktop.systemd1.Manager.xml
    dbus/org.freedesktop.systemd1.Mount.xml
    dbus/org.freedesktop.systemd1.Path.xml
    dbus/org.freedesktop.systemd1.Scope.xml
    dbus/org.freedesktop.systemd1.Service.xml
    dbus/org.freedesktop.systemd1.Slice.xml
    dbus/org.freedesktop.systemd1.Socket.xml
    dbus/org.freedesktop.systemd1.Swap.xml
    dbus/org.freedesktop.systemd1.Target.xml
    dbus/org.freedesktop.systemd1.Timer.xml
    dbus/org.freedesktop.systemd1.Unit.xml
    dbus/org.freedesktop.DBus.Properties.xml
)

set_property(SOURCE ${INTERFACE_INTROSPECTION_XML_FILES}
              PROPERTY INCLUDE generic-types.h)

set_source_files_properties(${INTERFACE_INTROSPECTION_XML_FILES}
                               PROPERTIES NO_NAMESPACE TRUE)

qt_add_dbus_interfaces(QtSystemd_PART_SRCS ${INTERFACE_INTROSPECTION_XML_FILES})

add_library(QtSystemd SHARED ${QtSystemd_PART_SRCS})

qt5_use_modules(QtSystemd Core DBus)

set_property(TARGET QtSystemd PROPERTY COMPILE_DEFINITIONS MAKE_SDQT_LIB)
set_property(TARGET QtSystemd PROPERTY VERSION ${VERSION})
set_property(TARGET QtSystemd PROPERTY SOVERSION 0)

set_target_properties(QtSystemd PROPERTIES
  PUBLIC_HEADER "${QtSystemd_HEADERS}")

install(TARGETS QtSystemd
  # IMPORTANT: Add the QtSystemd library to the "export-set"
  EXPORT QtSystemdTargets
  RUNTIME DESTINATION "${INSTALL_BIN_DIR}" COMPONENT bin
  LIBRARY DESTINATION "${INSTALL_LIB_DIR}" COMPONENT shlib
  PUBLIC_HEADER DESTINATION "${INSTALL_INCLUDE_DIR}"
    COMPONENT dev)
