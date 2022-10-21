cmake_minimum_required(VERSION 3.14)

# set(CMAKE_CXX_STANDARD 17)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
# set(CMAKE_CXX_EXTENSIONS OFF)

project(project-generator)


# find_package(OpenSSL CONFIG REQUIRED)
# message("OpenSSL found: ${OpenSSL_FOUND}")
# # set(OpenSSL::Crypto Crypto)

find_package(Poco REQUIRED COMPONENTS Net Util JSON) 
if (Poco_FOUND)
    message("Poco found")
else (Poco_FOUND)
    message("Poco not found")
endif()

find_package(nlohmann_json 3.11.2 EXACT REQUIRED)
if (nlohmann_json_FOUND)
    message("nlohmann_json found")
else (nlohmann_json_FOUND)
    message("nlohmann_json not found")
endif()

find_package(pugixml 1.12 EXACT REQUIRED)
if (pugixml_FOUND)
    message("pugixml found")
else (pugixml_FOUND)
    message("pugixml not found")
endif()

SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static")

add_executable(${PROJECT_NAME}
    "src/main.cpp"
    "src/utils/Utils.h"
    "src/utils/Utils.cpp"
)

target_link_libraries(${PROJECT_NAME} Poco::Util Poco::JSON Poco::Net nlohmann_json::nlohmann_json pugixml::static)