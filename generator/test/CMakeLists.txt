set(CMAKE_POSITION_INDEPENDENT_CODE ON)

if (NOT DEFINED CMAKE_INSTALL_BINDIR)
    include(GNUInstallDirs)
endif()

function(vpGeneratorTest NAME)
    set(TEST_FILE ./${NAME}.cpp)
    set(TEST_NAME ${NAME})

    add_executable(${TEST_NAME} ${TEST_FILE})
    target_link_libraries(${TEST_NAME} gtest gtest_main)
    if(WIN32)
        target_link_libraries(${TEST_NAME} Cfgmgr32)
    endif()
    add_test(NAME ${TEST_NAME} COMMAND ${TEST_NAME})
    set_target_properties(${TEST_NAME} PROPERTIES FOLDER "Profiles generator/Tests")
endfunction(vpGeneratorTest)

vpGeneratorTest(test_util)
