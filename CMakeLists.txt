set(CMAKE_CXX_STANDARD 14)

__cc_find(Clipper3r)
__assert_target(clipper3r)
__cc_find(Nlopt)
__assert_target(nlopt)
#__cc_find(Boost)

set(LIBNEST2D_SRCFILES
    include/libnest2d/libnest2d.hpp
    include/libnest2d/nester.hpp
    include/libnest2d/geometry_traits.hpp
    include/libnest2d/geometry_traits_nfp.hpp
    include/libnest2d/common.hpp
    include/libnest2d/optimizer.hpp
    include/libnest2d/utils/metaloop.hpp
    include/libnest2d/utils/rotfinder.hpp
    include/libnest2d/utils/rotcalipers.hpp
    include/libnest2d/placers/placer_boilerplate.hpp
    include/libnest2d/placers/bottomleftplacer.hpp
    include/libnest2d/placers/nfpplacer.hpp
    include/libnest2d/selections/selection_boilerplate.hpp
    #include/libnest2d/selections/filler.hpp
    include/libnest2d/selections/firstfit.hpp
    #include/libnest2d/selections/djd_heuristic.hpp
    include/libnest2d/backends/clipper/geometries.hpp
    include/libnest2d/backends/clipper/clipper_polygon.hpp
    include/libnest2d/optimizers/nlopt/nlopt_boilerplate.hpp
    include/libnest2d/optimizers/nlopt/simplex.hpp
    include/libnest2d/optimizers/nlopt/subplex.hpp
    include/libnest2d/optimizers/nlopt/genetic.hpp
    src/libnest2d.cpp
    include/libnest2d/nfp/libnfporb.hpp
    )

set(LIBS clipper3r nlopt polygonLib)
set(DEFS LIBNEST2D_STATIC LIBNEST2D_OPTIMIZER_nlopt LIBNEST2D_GEOMETRIES_clipper)
set(INCS ${CMAKE_CURRENT_SOURCE_DIR}/include/)
if(BOOST_INCLUDE_DIRS)
	list(APPEND INCS ${BOOST_INCLUDE_DIRS})
endif()

if(TARGET tbb)
	list(APPEND LIBS tbb)
	list(APPEND DEFS USE_TBB)
endif()
__add_real_target(libnest2d lib SOURCE ${LIBNEST2D_SRCFILES}
								LIB ${LIBS}
								DEF ${DEFS}
								INC ${INCS}
								INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/include/)

if(CC_INSTALL_LIBNEST2D)
	__install_directory_specif(${CMAKE_CURRENT_SOURCE_DIR}/include/ libnest2d)
endif()