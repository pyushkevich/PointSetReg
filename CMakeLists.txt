CMAKE_MINIMUM_REQUIRED(VERSION 2.6.2)
IF(COMMAND CMAKE_POLICY)
  CMAKE_POLICY(SET CMP0003 NEW)
ENDIF(COMMAND CMAKE_POLICY)  

PROJECT(POINTSET)

FIND_PACKAGE(ITK REQUIRED)
INCLUDE(${ITK_USE_FILE})

FIND_PACKAGE(VTK REQUIRED)
INCLUDE(${VTK_USE_FILE})

INCLUDE_DIRECTORIES(${POINTSET_SOURCE_DIR})

ADD_EXECUTABLE(ml_affine MultiLabelAffine.cxx)

# Avoid having to link with OpenGL, etc
SET(VTK_LIBRARIES
   vtkCommonCore vtkCommonMath vtkCommonMisc vtkCommonSystem vtkCommonTransforms 
   vtkCommonDataModel vtkCommonColor vtkCommonExecutionModel vtkFiltersCore 
   vtkCommonComputationalGeometry vtkFiltersGeneral vtkImagingCore
   vtkIOCore vtkIOGeometry vtkIOImage vtkIOLegacy)

SET(COMMON_LIBS
  ${ITK_LIBRARIES}
  ${VTK_LIBRARIES}
)

TARGET_LINK_LIBRARIES(ml_affine ${COMMON_LIBS})
