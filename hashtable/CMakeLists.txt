add_executable(HashTable)


set(SourceDir "src/")
set(CompilationUnits "HashTable.cpp;CSVparser.cpp")
list(TRANSFORM CompilationUnits PREPEND ${SourceDir})

set(HeaderDir "include/")
set(HeaderFiles "CSVparser.hpp")
list(TRANSFORM HeaderFiles PREPEND ${HeaderDir})

target_sources(
        HashTable
        PRIVATE
        ${CompilationUnits}

        PRIVATE
        FILE_SET HEADERS
        BASE_DIRS ${HeaderDir}
        FILES ${HeaderFiles}
)

target_include_directories(
        HashTable PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

target_link_libraries(
        HashTable PRIVATE
        StrictWarnings
)

# Copy the csv file into the directory of exec for testing
add_custom_command(
        TARGET HashTable POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${CMAKE_CURRENT_SOURCE_DIR}/eBid_Monthly_Sales.csv"
        "$<TARGET_FILE_DIR:HashTable>/eBid_Monthly_Sales.csv"
)