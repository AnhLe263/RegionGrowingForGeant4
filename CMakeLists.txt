project(LabellingFIlter)  
cmake_minimum_required(VERSION 3.8)
aux_source_directory(. SRC_LIST)
#################################################################################################################
set(VTK_DIR "/usr/local/itkvtk/lib/cmake/vtk-8.2/")
find_package(VTK COMPONENTS
  vtkCommonCore
  vtkFiltersSources
  vtkGUISupportQt
  vtkIOImage
  vtkInteractionImage
)
include(${VTK_USE_FILE})
###########################################################################################################
find_package(ITK REQUIRED)
include(${ITK_USE_FILE})
###########################################################################################################
find_package(Geant4 REQUIRED ui_all vis_all)
include(${Geant4_USE_FILE})
#################################################################################################################
include_directories(${PROJECT_SOURCE_DIR}/include
                    ${Geant4_INCLUDE_DIR})
#################################################################################################################
file(GLOB sources ${PROJECT_SOURCE_DIR}/src/*.cpp)
file(GLOB headers ${PROJECT_SOURCE_DIR}/include/*.hh)
#################################################################################################################
add_executable(${PROJECT_NAME} ${SRC_LIST} ${sources} ${headers})
target_link_libraries(${PROJECT_NAME} ${VTK_LIBRARIES} ${ITK_LIBRARIES} ${Geant4_LIBRARIES})
