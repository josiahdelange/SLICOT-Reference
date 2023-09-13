set(CMAKE_Fortran_MODULE_DIRECTORY ${CMAKE_BINARY_DIR}/modules)

# External/auxillary source files
set(SLICOT_EXTERNAL ${SLICOT_EXTERNAL}
    dlatzm.f
    zlatzm.f
)

# Build the auxillary library
add_library(lpkaux ${SLICOT_EXTERNAL} ${BLAS_LIBRARIES} ${LAPACK_LIBRARIES})
set_target_properties(lpkaux PROPERTIES LINKER_LANGUAGE Fortran)
