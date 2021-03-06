project(java-tools NONE)

configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/bin/pki.in
    ${CMAKE_CURRENT_BINARY_DIR}/bin/pki
)

add_custom_target(pki-tools-man ALL
    COMMENT "Creating PKI tools manuals")

add_custom_command(
    TARGET pki-tools-man
    COMMAND ${CMAKE_COMMAND} -E make_directory ${CMAKE_CURRENT_BINARY_DIR}/man/man1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/AtoB.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/AtoB.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/AuditVerify.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/AuditVerify.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/BtoA.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/BtoA.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/CMCEnroll.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/CMCEnroll.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/CMCRequest.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/CMCRequest.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/CMCResponse.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/CMCResponse.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/CMCSharedToken.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/CMCSharedToken.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/KRATool.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/KRATool.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/PKCS10Client.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/PKCS10Client.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/PKICertImport.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/PKICertImport.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/PrettyPrintCert.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/PrettyPrintCert.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/PrettyPrintCrl.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/PrettyPrintCrl.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-audit.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-audit.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-ca-cert.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-ca-cert.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-ca-kraconnector.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-ca-kraconnector.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-ca-profile.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-ca-profile.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-client.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-client.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-group.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-group.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-group-member.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-group-member.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-kra-key.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-kra-key.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-pkcs12.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-pkcs12.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-pkcs12-cert.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-pkcs12-cert.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-pkcs12-key.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-pkcs12-key.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-securitydomain.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-securitydomain.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-tps-profile.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-tps-profile.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-user.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-user.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-user-cert.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-user-cert.1
    COMMAND go-md2man -in ${CMAKE_SOURCE_DIR}/docs/manuals/man1/pki-user-membership.1.md -out ${CMAKE_CURRENT_BINARY_DIR}/man/man1/pki-user-membership.1
)

# install man pages generated by md2man
install(
    DIRECTORY
        ${CMAKE_CURRENT_BINARY_DIR}/man/
    DESTINATION
        ${MAN_INSTALL_DIR}
    FILE_PERMISSIONS
        OWNER_READ OWNER_WRITE
        GROUP_READ
        WORLD_READ
)

# Create compatibility symlink for DRMTool.1.gz -> KRATool.1.gz

add_custom_target(pki-DRMTool-man-link ALL
    COMMENT "Creating link for DRMTool man page")

add_custom_command(
    TARGET pki-DRMTool-man-link
    COMMAND ln -sf ${MAN_INSTALL_DIR}/man1/KRATool.1.gz ${CMAKE_CURRENT_BINARY_DIR}/DRMTool.1.gz
)

install(
    FILES
        ${CMAKE_CURRENT_BINARY_DIR}/DRMTool.1.gz
    DESTINATION
        ${MAN_INSTALL_DIR}/man1
    PERMISSIONS
        OWNER_READ OWNER_WRITE
        GROUP_READ
        WORLD_READ
)

install(
    FILES
        ${CMAKE_CURRENT_BINARY_DIR}/bin/pki
    DESTINATION
        ${BIN_INSTALL_DIR}
    PERMISSIONS
        OWNER_EXECUTE OWNER_WRITE OWNER_READ
        GROUP_EXECUTE GROUP_READ
        WORLD_EXECUTE WORLD_READ
)

add_subdirectory(src)
add_subdirectory(templates)
