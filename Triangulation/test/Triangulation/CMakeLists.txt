# Created by the script cgal_create_cmake_script
# This is the CMake script for compiling a CGAL application.


project( Triangulation_test )

cmake_minimum_required(VERSION 2.8.11)


find_package(CGAL QUIET)

if ( CGAL_FOUND )

  include( ${CGAL_USE_FILE} )

  include( CGAL_CreateSingleSourceCGALProgram )
  
  find_package(Eigen3 3.1.0) 
  if (EIGEN3_FOUND) 
    include( ${EIGEN3_USE_FILE} ) 
    include_directories (BEFORE "../../include")
    include_directories (BEFORE "include")

    create_single_source_cgal_program( "test_delaunay.cpp" )
    create_single_source_cgal_program( "test_tds.cpp" )
    create_single_source_cgal_program( "test_torture.cpp" )
    create_single_source_cgal_program( "test_triangulation.cpp" )

  else()
    message(STATUS "NOTICE: Some of the executables in this directory need Eigen 3.1 (or greater) and will not be compiled.")
  endif()

else()
  
    message(STATUS "This program requires the CGAL library, and will not be compiled.")
  
endif()

