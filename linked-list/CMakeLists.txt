add_executable(LinkedList)


set(SourceDir "src/")
set(CompilationUnits "LinkedList.cpp;CSVparser.cpp")
list(TRANSFORM CompilationUnits PREPEND ${SourceDir})

set(HeaderDir "include/")
set(HeaderFiles "CSVparser.hpp")
list(TRANSFORM HeaderFiles PREPEND ${HeaderDir})

target_sources(
        LinkedList
        PRIVATE
        ${CompilationUnits}

        PRIVATE
        FILE_SET HEADERS
        BASE_DIRS ${HeaderDir}
        FILES ${HeaderFiles}
)

target_include_directories(
        LinkedList PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

target_link_libraries(
        LinkedList PRIVATE
        StrictWarnings
)

# Copy the csv file into the directory of exec for testing
add_custom_command(
        TARGET LinkedList POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${CMAKE_CURRENT_SOURCE_DIR}/eBid_Monthly_Sales.csv"
        "$<TARGET_FILE_DIR:LinkedList>/eBid_Monthly_Sales.csv"
)