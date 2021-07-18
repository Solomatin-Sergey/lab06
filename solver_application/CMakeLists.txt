cmake_minimum_required(VERSION 3.1)
# Добавляет определения в командную строку компилятора для целей в текущем каталоге.
# Эта команда предназначена для добавления определений препроцессора.
# Предполагалось, что следующий стандарт будет выпущен в 2008 году, но, поскольку он был неопределенным, он был назван C++0x, где x обозначает 8 или 9. 
add_definitions(-std=c++0x) 

project(S)
# Добавляются в сборку подключаемые каталоги.
include_directories(solver_lib) 
include_directories(formatter_ex_lib) 
# Добавляется подкаталог в сборку. Source_dir указывает каталог, в котором находятся исходный файл CMakeLists.txt и файлы кода.
add_subdirectory(solver_lib)
add_subdirectory(formatter_ex_lib)

add_executable(solver equation.cpp)

target_link_libraries(solver solver_lib)
target_link_libraries(solver formatter_ex)
# Эта команда генерирует правила установки для проекта;  bin - каталог на диске, в который будет установлен файл.
install(TARGETS solver DESTINATION bin)

set(CPACK_PACKAGE_NAME "solver") # Название пакета (или приложения). Если не указано, то по умолчанию используется название проекта.
set(CPACK_PACKAGE_VENDOR "SuperCompany") # Имя поставщика пакета (например,"Kitware").По умолчанию используется "Humanity".
set(CPACK_PACKAGE_CONTACT "some contact")  
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Nightmare") # если CPACK_DEBIAN_PACKAGE_MAINTAINER не установлен,
# вместо него будет использоваться CPACK_PACKAGE_CONTACT
set(CPACK_PACKAGE_DESCRIPTION "What's up, guys? :-)") # описание проекта
set(CPACK_GENERATOR "DEB" "RPM") #  CPACK_GENERATOR-это список генераторов: 
# и когда cpack запускается без других аргументов, он проходится по списку и создает по одному пакету для каждого генератора. 

include(CPack) # Если CMake запускается с помощью генератора ( например, Makefile, Ninja или Xcode) то include(CPack) создает целевой пакет.