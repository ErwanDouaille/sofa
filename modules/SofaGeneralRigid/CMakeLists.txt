cmake_minimum_required(VERSION 3.1)
project(SofaGeneralRigid)

message(STATUS "SofaGeneralRigid:")
################################ COMPONENTS HERE ARE THE NG-SET ####################################
set(HEADER_FILES
   config.h
    initGeneralRigid.h
)

set(SOURCE_FILES
    initGeneralRigid.cpp
)

############################## COMPONENTS HERE ARE THE LIGHT-SET ###################################
if(SOFA_BUILD_COMPONENTSET_LIGHT)
    list(APPEND HEADER_FILES

        )
    list(APPEND SOURCE_FILES

        )
endif()

############################## COMPONENTS HERE ARE THE STANDARD-SET ################################
if(SOFA_BUILD_COMPONENTSET_STANDARD)
    list(APPEND HEADER_FILES
        ArticulatedHierarchyContainer.h
        ArticulatedHierarchyContainer.inl
        ArticulatedSystemMapping.h
        ArticulatedSystemMapping.inl
        LineSetSkinningMapping.h
        LineSetSkinningMapping.inl
        SkinningMapping.h
        SkinningMapping.inl
        )
    list(APPEND SOURCE_FILES
        ArticulatedHierarchyContainer.cpp
        ArticulatedSystemMapping.cpp
        LineSetSkinningMapping.cpp
        SkinningMapping.cpp
        )
endif()

############################### COMPONENTS HERE ARE DEPRECATED ####################################
if(SOFA_BUILD_COMPONENTSET_FULL)

endif()


add_library(${PROJECT_NAME} SHARED ${HEADER_FILES} ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME} PUBLIC SofaBaseMechanics)
set_target_properties(${PROJECT_NAME} PROPERTIES COMPILE_FLAGS "-DSOFA_BUILD_GENERAL_RIGID")
set_target_properties(${PROJECT_NAME} PROPERTIES PUBLIC_HEADER "${HEADER_FILES}")

sofa_install_targets(SofaGeneral ${PROJECT_NAME} ${PROJECT_NAME})
