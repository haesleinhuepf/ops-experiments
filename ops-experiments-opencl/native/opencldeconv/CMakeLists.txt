find_package(OpenCL)

if (${CMAKE_SYSTEM_NAME} STREQUAL "Windows")
    FIND_PATH(OPENCL_INCLUDE_DIR ENV{OPENCL_INCLUDE_DIR} [DOC "Open CL include path"])
    include_directories( ${OPENCL_INCLUDE_DIR} )
endif()

# find clFFT path
FIND_PATH(CLFFT_LIBRARY_DIR $ENV{CLFFT_LIBRARY_DIR} [DOC "CLFFT library path"])

link_directories(/Users/haase/code/ops-experiments/ops-experiments-opencl/native ${CLFFT_LIBRARY_DIR})
add_library(opencldeconv SHARED opencldeconv.cpp)
target_link_libraries(opencldeconv clFFT ${OpenCL_LIBRARY})

install(TARGETS opencldeconv DESTINATION lib)