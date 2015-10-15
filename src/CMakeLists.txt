file(GLOB files "${CMAKE_CURRENT_SOURCE_DIR}/16x16/*.png")
install(FILES ${files} DESTINATION share/icons/hicolor/16x16/mimetypes/)

file(GLOB files "${CMAKE_CURRENT_SOURCE_DIR}/22x22/*.png")
install(FILES ${files} DESTINATION share/icons/hicolor/22x22/mimetypes/)

file(GLOB files "${CMAKE_CURRENT_SOURCE_DIR}/32x32/*.png")
install(FILES ${files} DESTINATION share/icons/hicolor/32x32/mimetypes/)

file(GLOB files "${CMAKE_CURRENT_SOURCE_DIR}/48x48/*.png")
install(FILES ${files} DESTINATION share/icons/hicolor/48x48/mimetypes/)

file(GLOB files "${CMAKE_CURRENT_SOURCE_DIR}/64x64/*.png")
install(FILES ${files} DESTINATION share/icons/hicolor/64x64/mimetypes/)

install(FILES neurosuite-mime.xml DESTINATION share/mime/packages/)
