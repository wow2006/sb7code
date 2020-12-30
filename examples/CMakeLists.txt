# ${}/examples/CMakeLists.txt
set(
  EXAMPLES
  alienrain
  basicfbo
  bindlesstex
  blendmatrix
  blinnphong
  bumpmapping
  clipdistance
  csflocking
  compressrgtc
  cubemapenv
  cubicbezier
  cullindirect
  deferredshading
  depthclamp
  dflandscape
  dispmap
  dof
  envmapsphere
  equirectangular
  fontdemo
  fragcolorfrompos
  fragmentlist
  grass
  gsculling
  gslayered
  gsquads
  gstessellate
  hdrbloom
  hdrexposure
  hdrtonemap
  hqfilter
  indexedcube
  indirectmaterial
  instancedattribs
  julia
  ktxview
  linesmooth
  mirrorclampedge
  movingtri
  msaanative
  multidrawindirect
  multiscissor
  multiviewport
  noperspective
  normalviewer
  objectexploder
  ompparticles
  packetbuffer
  perpixelgloss
  phonglighting
  polygonsmooth
  prefixsum
  pmbfractal
  pmbstreaming
  prefixsum2d
  programinfo
  raytracer
  rimlight
  sampleshading
# sb6mrender
  sdfdemo
  shadowmapping
  shapedpoints
  simpleclear
  simpletexcoords
  simpletexture
  singlepoint
  singletri
  sparsetexture
  spinnycube
  springmass
  ssao
  starfield
  stereo
  subroutines
  tessellatedcube
  tessellatedgstri
  tessellatedtri
  tessmodes
  tesssubdivmodes
  toonshading
  tunnel
  wrapmodes
)

find_package(OpenMP)

foreach(EXAMPLE IN LISTS EXAMPLES)
  add_executable(
    ${EXAMPLE}
    WIN32
    ${EXAMPLE}/${EXAMPLE}.cpp
  )

  set_property(
    TARGET ${EXAMPLE}
    PROPERTY DEBUG_POSTFIX _d
  )

  target_link_libraries(
    ${EXAMPLE}
    PUBLIC
    sb7
    OpenMP::OpenMP_CXX
  )

  if(MSVC)
    configure_file(
      ${PROJECT_SOURCE_DIR}/build/templates/vs2013.vcxproj.user.in
      ${CMAKE_CURRENT_BINARY_DIR}/${EXAMPLE}.vcxproj.user @ONLY
    )
  endif()
endforeach()

IF (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_LINUX -std=c++0x")
ENDIF (${CMAKE_SYSTEM_NAME} MATCHES "Linux")

include_directories( include )

ADD_CUSTOM_TARGET(debug ${CMAKE_COMMAND} -DCMAKE_BUILD_TYPE:STRING=Debug ${PROJECT_SOURCE_DIR})
ADD_CUSTOM_TARGET(release ${CMAKE_COMMAND} -DCMAKE_BUILD_TYPE:STRING=Release ${PROJECT_SOURCE_DIR})
