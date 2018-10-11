add_subdirectory("os")
add_subdirectory("base")
add_subdirectory("ini")

ADD_LIBRARY(license++_static STATIC
    license++.cpp
    LicenseReader.cpp
    pc-identifiers.c
)

target_link_libraries(
     license++_static
     ini
     os
)


ADD_LIBRARY(license2++_static STATIC 
    license++.cpp
    LicenseReader.cpp
    pc-identifiers.c
    ini/ConvertUTF.c
    os/os.c
    os/os-win.c
    base/EventRegistry.cpp
    base/StringUtils.cpp
    base/logger.c
    ../tools/base_lib/CryptoHelper.cpp
    ../tools/base_lib/win/CryptoHelperWindows.cpp
)

install(TARGETS license++_static ARCHIVE DESTINATION lib)
install(FILES api/datatypes.h api/license++.h DESTINATION include/api)
install(FILES base/base.h DESTINATION include/base)
install(FILES pc-identifiers.h DESTINATION include/)
