add_executable(VectorSorting)


set(SourceDir "src/")
set(CompilationUnits "VectorSorting.cpp;CSVparser.cpp")
list(TRANSFORM CompilationUnits PREPEND ${SourceDir})

set(HeaderDir "include/")
set(HeaderFiles "CSVparser.hpp")
list(TRANSFORM HeaderFiles PREPEND ${HeaderDir})

target_sources(
        VectorSorting
        PRIVATE
        ${CompilationUnits}

        PRIVATE
        FILE_SET HEADERS
        BASE_DIRS ${HeaderDir}
        FILES ${HeaderFiles}
)

target_include_directories(
        VectorSorting PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

target_link_libraries(
        VectorSorting PRIVATE
        StrictWarnings
)