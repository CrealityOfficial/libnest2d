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
    )

__add_real_target(libnest2d lib SOURCE ${LIBNEST2D_SRCFILES}
								LIB clipperz tbb nlopt
								DEF USE_TBB LIBNEST2D_STATIC LIBNEST2D_OPTIMIZER_nlopt LIBNEST2D_GEOMETRIES_clipper
								INC ${CMAKE_CURRENT_SOURCE_DIR}/include/ ${BOOST_INCLUDES}
								INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/include/)

