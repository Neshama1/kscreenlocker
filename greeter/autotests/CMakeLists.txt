add_definitions(-DKSCREENLOCKER_UNIT_TEST)
include(ECMMarkAsTest)
find_package(Qt5 ${QT_MIN_VERSION} CONFIG REQUIRED COMPONENTS DBus Quick )
#####################################
# fakekcheckpass
#####################################
add_executable(fakekcheckpass fakekcheckpass.c)
ecm_mark_nongui_executable(fakekcheckpass)
target_link_libraries(fakekcheckpass ${SOCKET_LIBRARIES})

#######################################
# AuthenticatorTest
#######################################
set( authenticatorTest_SRCS
     authenticatortest.cpp
     ../authenticator.cpp
)
add_executable(authenticatorTest ${authenticatorTest_SRCS})
target_link_libraries(authenticatorTest Qt5::Test Qt::DBus)
add_test(NAME ksmserver-authenticatorTest COMMAND authenticatorTest)
ecm_mark_as_test(authenticatorTest)

#######################################
# KillTest
#######################################
add_executable(killTest killtest.cpp)
add_test(NAME kscreenlocker-killTest COMMAND killTest)
ecm_mark_as_test(killTest)
target_link_libraries(killTest Qt5::Test Qt::DBus)
