add_definitions(-DKSCREENLOCKER_UNIT_TEST)
include(ECMMarkAsTest)

#######################################
# LogindTest
#######################################
set(logindTest_SRCS
    logindtest.cpp
    fakelogind.cpp
    ../logind.cpp
    ../kscreenlocker_logging.cpp
)

add_executable(logindTest ${logindTest_SRCS})
target_link_libraries(logindTest Qt5::DBus Qt5::Test KF5::I18n)
add_test(NAME ksmserver-logindTest COMMAND logindTest)
ecm_mark_as_test(logindTest)

#######################################
# KSldTest
#######################################
add_executable(ksldTest ksldtest.cpp)
target_link_libraries(ksldTest Qt5::Test Qt5::Widgets KF5::IdleTime XCB::XTEST KScreenLocker)
add_test(NAME ksmserver-ksldTest COMMAND ksldTest)
ecm_mark_as_test(ksldTest)

#######################################
# KeyboardGrabber
#######################################
add_executable(keyboardGrabber keyboardgrabber.cpp)
target_link_libraries(keyboardGrabber Qt5::Core XCB::XCB)
ecm_mark_as_test(keyboardGrabber)

#######################################
# PointerGrabber
#######################################
add_executable(pointerGrabber pointergrabber.cpp)
target_link_libraries(pointerGrabber Qt5::Core XCB::XCB)
ecm_mark_as_test(pointerGrabber)

#######################################
# LockWindowTest
#######################################
set(x11LockerTest_SRCS
    x11lockertest.cpp
    ../x11locker.cpp
    ../globalaccel.cpp
    ../abstractlocker.cpp
    ../kscreenlocker_logging.cpp
)

add_executable(x11LockerTest ${x11LockerTest_SRCS})
target_link_libraries(x11LockerTest
    KF5::GlobalAccel
    KF5::I18n
    KF5::WindowSystem
    Qt5::Test
    Qt5::X11Extras
    Qt5::Widgets
    ${X11_LIBRARIES}
    XCB::XCB
    XCB::KEYSYMS
)
add_test(NAME ksmserver-x11LockerTest COMMAND x11LockerTest)
ecm_mark_as_test(x11LockerTest)

#######################################
# NoScreensTest
#######################################
set(noScreensTest_SRCS noscreens.cpp)
add_executable(noScreensTest ${noScreensTest_SRCS})
target_link_libraries(noScreensTest
    KScreenLocker
    Qt5::Test
    KF5::WaylandServer
    )
add_test(NAME ksld-noScreensTest COMMAND noScreensTest)
ecm_mark_as_test(noScreensTest)
