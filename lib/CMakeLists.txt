#Bundler libs

# 5point
if (5point)
	file(GLOB 5POINT_SRC_C_H "${BUNDLER_LIB_PATH}/5point/*.c" "${BUNDLER_LIB_PATH}/5point/*.h")
	set(5POINT_SRCS
		${5POINT_SRC_C_H})

	add_library (5point STATIC
		${5POINT_SRCS})

	target_include_directories(5point PRIVATE
		${BUNDLER_INCLUDE_PATH}
		${BUNDLER_LIB_PATH}/imagelib
		${BUNDLER_LIB_PATH}/matrix)
endif (5point)

# ann_1.1_char
if (ann_1.1_char)
	file(GLOB ANN_1.1_CHAR_SRC_C_H "${BUNDLER_LIB_PATH}/ann_1.1_char/src/*.cpp" "${BUNDLER_LIB_PATH}/ann_1.1_char/src/*.h")
	set(ANN_1.1_CHAR_SRCS	
		${BUNDLER_LIB_PATH}/ann_1.1_char/include/ANN/ANN.H
		${BUNDLER_LIB_PATH}/ann_1.1_char/include/ANN/ANNx.H
		${ANN_1.1_CHAR_SRC_C_H})

	add_library (ann_1.1_char SHARED
		${ANN_1.1_CHAR_SRCS})

	set_target_properties(ann_1.1_char 
		PROPERTIES 
		COMPILE_DEFINITIONS "_LIB;_USRDLL;DLL_EXPORTS;ANN_PERF;ANN_NO_RANDOM")

	target_include_directories(ann_1.1_char PRIVATE
		${BUNDLER_LIB_PATH}/ann_1.1_char/include)
endif (ann_1.1_char)

# cblas
if (cblas)
	file(GLOB CBLAS_SRC_C_H "${BUNDLER_LIB_PATH}/cblas/*.c" "${BUNDLER_LIB_PATH}/cblas/*.h")
	set(CBLAS_SRCS
		${CBLAS_SRC_C_H})

	add_library (cblas STATIC
		${CBLAS_SRCS})

	set_target_properties(cblas
		PROPERTIES 
		COMPILE_DEFINITIONS "_LIB;NO_BLAS_WRAP")
endif (cblas)

# clapack
if (clapack)
	file(GLOB CLAPACK_BLAS_C_H "${BUNDLER_LIB_PATH}/clapack/BLAS/SRC/*.c" "${BUNDLER_LIB_PATH}/clapack/BLAS/SRC/*.h")
	file(GLOB CLAPACK_SRC_C_H "${BUNDLER_LIB_PATH}/clapack/SRC/*.c"  "${BUNDLER_LIB_PATH}/clapack/SRC/*.h")

	set(CLAPACK_SRCS
		${CLAPACK_BLAS_C_H}
		${CLAPACK_SRC_C_H}
		${BUNDLER_LIB_PATH}/clapack/INSTALL/dlamch.c
		${BUNDLER_LIB_PATH}/clapack/INSTALL/dlamchtst.c
		${BUNDLER_LIB_PATH}/clapack/INSTALL/dsecndtst.c
		${BUNDLER_LIB_PATH}/clapack/INSTALL/ilaver.c
		${BUNDLER_LIB_PATH}/clapack/INSTALL/LAPACK_version.c
		${BUNDLER_LIB_PATH}/clapack/INSTALL/lsame.c
		${BUNDLER_LIB_PATH}/clapack/INSTALL/lsametst.c
		${BUNDLER_LIB_PATH}/clapack/INSTALL/tstiee.c)

	add_library(clapack STATIC
		${CLAPACK_SRCS})

	set_target_properties(clapack
		PROPERTIES 
		COMPILE_DEFINITIONS "_LIB;NO_BLAS_WRAP")

	target_include_directories(clapack PRIVATE
		${BUNDLER_LIB_PATH}/f2c)
endif (clapack)

# cminpack
if (cminpack)
	file(GLOB CMINPACK_SRC_C_H "${BUNDLER_LIB_PATH}/cminpack/*.c" "${BUNDLER_LIB_PATH}/cminpack/*.h")
	set(CMINPACK_SRCS
		${CMINPACK_SRC_C_H})

	add_library(cminpack STATIC
		${CMINPACK_SRCS})

	target_include_directories(cminpack PRIVATE
		${BUNDLER_LIB_PATH}/f2c)
endif (cminpack)

# f2c
if (f2c)
	file(GLOB F2C_SRC_C "${BUNDLER_LIB_PATH}/f2c/*.c")
	file(GLOB F2C_SRC_H "${BUNDLER_LIB_PATH}/f2c/*.h")

	# exclude transform3D.c/transform-opt.c/pyramid-io.c
	LIST(REMOVE_ITEM F2C_SRC_C
		${BUNDLER_LIB_PATH}/f2c/c_abs.c
		${BUNDLER_LIB_PATH}/f2c/c_cos.c
		${BUNDLER_LIB_PATH}/f2c/c_div.c
		${BUNDLER_LIB_PATH}/f2c/c_exp.c
		${BUNDLER_LIB_PATH}/f2c/c_log.c
		${BUNDLER_LIB_PATH}/f2c/c_sin.c
		${BUNDLER_LIB_PATH}/f2c/c_sqrt.c
		${BUNDLER_LIB_PATH}/f2c/ftell64_.c
		${BUNDLER_LIB_PATH}/f2c/pow_qq.c
		${BUNDLER_LIB_PATH}/f2c/qbitbits.c
		${BUNDLER_LIB_PATH}/f2c/qbitshft.c)
	message("exclude ${BUNDLER_LIB_PATH}/f2c/c_abs.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/c_cos.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/c_div.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/c_exp.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/c_log.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/c_sin.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/c_sqrt.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/ftell64_.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/pow_qq.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/qbitbits.c")
	message("exclude ${BUNDLER_LIB_PATH}/f2c/qbitshft.c")

	set(F2C_SRCS
		${F2C_SRC_C}
		${F2C_SRC_H})

	add_library(f2c STATIC
		${F2C_SRCS})
endif (f2c)

# getopt
if (getopt)
	set(GETOPT_SRCS
		${BUNDLER_LIB_PATH}/getopt/getopt.c
		${BUNDLER_LIB_PATH}/getopt/getopt.h)

	add_library(getopt STATIC
		${GETOPT_SRCS})
endif (getopt)

# imagelib
if (imagelib)
	file(GLOB IMAGELIB_SRC_C "${BUNDLER_LIB_PATH}/imagelib/*.c")
	file(GLOB IMAGELIB_SRC_H "${BUNDLER_LIB_PATH}/imagelib/*.h")

	# exclude transform3D.c/transform-opt.c/pyramid-io.c
	LIST(REMOVE_ITEM IMAGELIB_SRC_C
		${BUNDLER_LIB_PATH}/imagelib/transform3D.c
		${BUNDLER_LIB_PATH}/imagelib/transform-opt.c
		${BUNDLER_LIB_PATH}/imagelib/pyramid-io.c)
	message("exclude ${BUNDLER_LIB_PATH}/imagelib/transform3D.c")
	message("exclude ${BUNDLER_LIB_PATH}/imagelib/transform-opt.c")
	message("exclude ${BUNDLER_LIB_PATH}/imagelib/pyramid-io.c")
	
	set(IMAGELIB_SRCS
		${IMAGELIB_SRC_H}
		${IMAGELIB_SRC_C})

	add_library(imagelib STATIC
		${IMAGELIB_SRCS})

	target_include_directories(imagelib PRIVATE
		${BUNDLER_INCLUDE_PATH}
		${BUNDLER_LIB_PATH}/matrix)
endif (imagelib)

# jpeg
if (jpeg)
	file(GLOB JPEG_SRC_C_H "${BUNDLER_LIB_PATH}/jpeg/src/*.c"  "${BUNDLER_LIB_PATH}/jpeg/src/*.h")
	set(JPEG_SRCS
		${JPEG_SRC_C_H})

	add_library(jpeg SHARED
		${JPEG_SRCS})

	set_target_properties(jpeg
		PROPERTIES 
		COMPILE_DEFINITIONS "_USRDLL;JPEG_EXPORTS")
endif (jpeg)

# matrix
if (matrix)
	file(GLOB MATRIX_SRC_C_H "${BUNDLER_LIB_PATH}/matrix/*.c" "${BUNDLER_LIB_PATH}/matrix/*.h")
	set(MATRIX_SRCS
		${MATRIX_SRC_C_H})

	add_library(matrix STATIC
		${MATRIX_SRCS})

	target_include_directories(matrix PRIVATE
		${BUNDLER_LIB_PATH}/imagelib
		${BUNDLER_INCLUDE_PATH})
endif (matrix)

# sba-1.5
if (sba-1.5)
	file(GLOB SBA-1.5_SRC_C_H "${BUNDLER_LIB_PATH}/sba-1.5/*.c" "${BUNDLER_LIB_PATH}/sba-1.5/*.h")
	set(SBA-1.5_SRCS
		${SBA-1.5_SRC_C_H})

	add_library(sba-1.5 STATIC
		${SBA-1.5_SRCS})

	target_include_directories(sba-1.5 PRIVATE
		${BUNDLER_LIB_PATH}/matrix)
endif (sba-1.5)

# sfm-driver
if (sfm-driver)
	set(SFM-DRIVER_SRCS
		${BUNDLER_LIB_PATH}/sfm-driver/sfm.h
		${BUNDLER_LIB_PATH}/sfm-driver/sfm.c)

	add_library(sfm-driver STATIC
		${SFM-DRIVER_SRCS})

	target_include_directories(sfm-driver PRIVATE
		${BUNDLER_INCLUDE_PATH}
		${BUNDLER_LIB_PATH}/sba-1.5
		${BUNDLER_LIB_PATH}/matrix)
endif (sfm-driver)