############################################################################
# CMakeLists.txt file for building ROOT rootfit/histfactory package
# @author Pere Mato, CERN
############################################################################

if(mathmore OR ROOT_mathmore_FOUND)
  set(ROOT_MATHMORE_LIBRARY MathMore)
endif()

ROOT_STANDARD_LIBRARY_PACKAGE(HistFactory
  HEADERS
    RooStats/HistFactory/Asimov.h
    RooStats/HistFactory/Channel.h
    RooStats/HistFactory/ConfigParser.h
    RooStats/HistFactory/Data.h
    RooStats/HistFactory/EstimateSummary.h
    RooStats/HistFactory/FlexibleInterpVar.h
    RooStats/HistFactory/HistFactoryException.h
    RooStats/HistFactory/HistFactoryModelUtils.h
    RooStats/HistFactory/HistFactoryNavigation.h
    RooStats/HistFactory/HistFactorySimultaneous.h
    RooStats/HistFactory/HistoToWorkspaceFactoryFast.h
    RooStats/HistFactory/HistoToWorkspaceFactory.h
    RooStats/HistFactory/HistRef.h
    RooStats/HistFactory/LinInterpVar.h
    RooStats/HistFactory/MakeModelAndMeasurementsFast.h
    RooStats/HistFactory/Measurement.h
    RooStats/HistFactory/ParamHistFunc.h
    RooStats/HistFactory/PiecewiseInterpolation.h
    RooStats/HistFactory/PreprocessFunction.h
    RooStats/HistFactory/RooBarlowBeestonLL.h
    RooStats/HistFactory/Sample.h
    RooStats/HistFactory/Systematics.h
  SOURCES
    src/Asimov.cxx
    src/Channel.cxx
    src/ConfigParser.cxx
    src/Data.cxx
    src/EstimateSummary.cxx
    src/FlexibleInterpVar.cxx
    src/Helper.cxx
    src/Helper.h
    src/HistFactoryModelUtils.cxx
    src/HistFactoryNavigation.cxx
    src/HistFactorySimultaneous.cxx
    src/HistoToWorkspaceFactory.cxx
    src/HistoToWorkspaceFactoryFast.cxx
    src/HistRef.cxx
    src/LinInterpVar.cxx
    src/MakeModelAndMeasurements.cxx
    src/MakeModelAndMeasurementsFast.cxx
    src/Measurement.cxx
    src/ParamHistFunc.cxx
    src/PiecewiseInterpolation.cxx
    src/PreprocessFunction.cxx
    src/RooBarlowBeestonLL.cxx
    src/Sample.cxx
    src/Systematics.cxx
  DICTIONARY_OPTIONS
    "-writeEmptyRootPCM"
  BUILTINS
    GSL
  DEPENDENCIES
    RooFit
    RooFitCore
    Tree
    RIO
    Hist
    Matrix
    MathCore
    Minuit
    Foam
    Graf
    Gpad
    RooStats
    XMLParser
)

ROOT_EXECUTABLE(hist2workspace MakeModelAndMeasurements.cxx hist2workspace.cxx
                LIBRARIES HistFactory RooFit RooFitCore Tree RIO Matrix Hist
                   ${ROOT_MATHMORE_LIBRARY} ${GSL_LIBRARIES} MathCore Graf Gpad
                   Minuit Foam RooStats XMLParser
                BUILTINS GSL)

file(COPY config/prepareHistFactory DESTINATION  ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})
install(FILES ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/prepareHistFactory
                PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
                            GROUP_EXECUTE GROUP_READ
                            WORLD_EXECUTE WORLD_READ
                DESTINATION ${CMAKE_INSTALL_BINDIR})
