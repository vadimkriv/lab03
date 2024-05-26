## Laboratory work III

Данная лабораторная работа посвещена изучению систем автоматизации сборки проекта на примере **CMake**

```sh
$ open https://cmake.org/
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab03** на сервисе **GitHub**
- [ ] 2. Ознакомиться со ссылками учебного материала
- [ ] 3. Выполнить инструкцию учебного материала
- [ ] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**



## Report

```sh
vadim@vadim-VirtualBox:~$ export GITHUB_USERNAME=polenk0
vadim@vadim-VirtualBox:~$ cd ${GITHUB_USERNAME}/workspace
vadim@vadim-VirtualBox:~/polenk0/workspace$ pushd .
~/polenk0/workspace ~/polenk0/workspace
vadim@vadim-VirtualBox:~/polenk0/workspace$ source scripts/activate
vadim@vadim-VirtualBox:~/polenk0/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab02.git projects/lab03
Клонирование в «projects/lab03»...
remote: Enumerating objects: 18, done.
remote: Counting objects: 100% (18/18), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 18 (delta 1), reused 12 (delta 0), pack-reused 0
Получение объектов: 100% (18/18), готово.
Определение изменений: 100% (1/1), готово.
vadim@vadim-VirtualBox:~/polenk0/workspace$ cd projects/lab03
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ git remote remove origin
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03.git
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ g++ -std=c++11 -I./include -c sources/print.cpp
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ ls print.o
print.o
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ nm print.o | grep print
0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
000000000000002a T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ ar rvs print.a print.o
ar: создаётся print.a
a - print.o
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ file print.a
print.a: current ar archive
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ g++ -std=c++11 -I./include -c examples/example1.cpp
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ ls example1.o
example1.o
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ g++ example1.o print.a -o example1
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ ./example1 && echo
hello
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ g++ -std=c++11 -I./include -c examples/example2.cpp
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ nm example2.o
0000000000000000 V DW.ref.__gxx_personality_v0
                 U __gxx_personality_v0
0000000000000000 T main
                 U __stack_chk_fail
                 U _Unwind_Resume
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED2Ev
0000000000000000 n _ZNSt15__new_allocatorIcED5Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZSt21ios_base_library_initv
0000000000000000 r _ZStL19piecewise_construct
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ g++ example2.o print.a -o example2
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ ./example2
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat log.txt && echo
hello
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ rm -rf example1.o example2.o print.o
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ rm -rf print.a
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ rm -rf example1 example2
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ rm -rf log.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat > CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.4)
project(print)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 13.2.0
-- The CXX compiler identification is GNU 13.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.6s)
-- Generating done (0.0s)
-- Build files have been written to: /home/vadim/polenk0/workspace/projects/lab03/_build
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cmake --build _build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> target_link_libraries(example1 print)
target_link_libraries(example2 print)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cmake --build _build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/vadim/polenk0/workspace/projects/lab03/_build
[ 33%] Built target print
[ 50%] Building CXX object CMakeFiles/example1.dir/examples/example1.cpp.o
[ 66%] Linking CXX executable example1
[ 66%] Built target example1
[ 83%] Building CXX object CMakeFiles/example2.dir/examples/example2.cpp.o
[100%] Linking CXX executable example2
[100%] Built target example2
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cmake --build _build --target print
[100%] Built target print
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cmake --build _build --target example1
[ 50%] Built target print
[100%] Built target example1
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cmake --build _build --target example2
[ 50%] Built target print
[100%] Built target example2
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ ls -la _build/libprint.a
-rw-rw-r-- 1 vadim vadim 2238 мая 19 17:53 _build/libprint.a
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ _build/example1 && echo
hello
hello
Команда «hello» не найдена, но может быть установлена с помощью:
sudo snap install hello              # version 2.10, or
sudo apt  install hello              # version 2.10-3
sudo apt  install hello-traditional  # version 2.10-6
См. 'snap info hello', чтобы посмотреть дополнительные версии.
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ _build/example2
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat log.txt && echo
hello
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ rm -rf log.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ git clone https://github.com/tp-labs/lab03 tmp
Клонирование в «tmp»...
remote: Enumerating objects: 91, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61
Получение объектов: 100% (91/91), 1.02 МиБ | 1.36 МиБ/с, готово.
Определение изменений: 100% (41/41), готово.
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ mv -f tmp/CMakeLists.txt .
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ rm -rf tmp
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_EXAMPLES "Build examples" OFF)

project(print)

add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)

target_include_directories(print PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

if(BUILD_EXAMPLES)
  file(GLOB EXAMPLE_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/examples/*.cpp")
  foreach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
    get_filename_component(EXAMPLE_NAME ${EXAMPLE_SOURCE} NAME_WE)
    add_executable(${EXAMPLE_NAME} ${EXAMPLE_SOURCE})
    target_link_libraries(${EXAMPLE_NAME} print)
    install(TARGETS ${EXAMPLE_NAME}
      RUNTIME DESTINATION bin
    )
  endforeach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
endif()

install(TARGETS print
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
install(EXPORT print-config DESTINATION cmake)
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/vadim/polenk0/workspace/projects/lab03/_build
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ cmake --build _build --target install
[100%] Built target print
Install the project...
-- Install configuration: ""
-- Installing: /home/vadim/polenk0/workspace/projects/lab03/_install/lib/libprint.a
-- Installing: /home/vadim/polenk0/workspace/projects/lab03/_install/include
-- Installing: /home/vadim/polenk0/workspace/projects/lab03/_install/include/print.hpp
-- Installing: /home/vadim/polenk0/workspace/projects/lab03/_install/cmake/print-config.cmake
-- Installing: /home/vadim/polenk0/workspace/projects/lab03/_install/cmake/print-config-noconfig.cmake
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ tree _install
_install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

4 directories, 4 files
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ git add CMakeLists.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ git commit -m"added CMakeLists.txt"
[master a9e747b] added CMakeLists.txt
 1 file changed, 36 insertions(+)
 create mode 100644 CMakeLists.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ git push origin master
Перечисление объектов: 21, готово.
Подсчет объектов: 100% (21/21), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (15/15), готово.
Запись объектов: 100% (21/21), 4.06 КиБ | 4.06 МиБ/с, готово.
Всего 21 (изменений 3), повторно использовано 16 (изменений 1), повторно использовано пакетов 0
remote: Resolving deltas: 100% (3/3), done.
To https://github.com/polenk0/lab03.git
 * [new branch]      master -> master
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab03$ popd
~/polenk0/workspace
vadim@vadim-VirtualBox:~/polenk0/workspace$ export LAB_NUMBER=03
vadim@vadim-VirtualBox:~/polenk0/workspace$ mkdir reports/lab${LAB_NUMBER}
vadim@vadim-VirtualBox:~/polenk0/workspace$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
cp: не удалось выполнить stat для 'tasks/lab03/README.md': Нет такого файла или каталога
vadim@vadim-VirtualBox:~/polenk0/workspace$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
vadim@vadim-VirtualBox:~/polenk0/workspace$ cd reports/lab${LAB_NUMBER}
vadim@vadim-VirtualBox:~/polenk0/workspace/reports/lab03$ edit REPORT.md

```

## Homework

Представьте, что вы стажер в компании "Formatter Inc.".
### Задание 1
Вам поручили перейти на систему автоматизированной сборки **CMake**.
Исходные файлы находятся в директории [formatter_lib](formatter_lib).
В этой директории находятся файлы для статической библиотеки *formatter*.
Создайте `CMakeList.txt` в директории [formatter_lib](formatter_lib),
с помощью которого можно будет собирать статическую библиотеку *formatter*.

### Задание 2
У компании "Formatter Inc." есть перспективная библиотека,
которая является расширением предыдущей библиотеки. Т.к. вы уже овладели
навыком созданием `CMakeList.txt` для статической библиотеки *formatter*, ваш 
руководитель поручает заняться созданием `CMakeList.txt` для библиотеки 
*formatter_ex*, которая в свою очередь использует библиотеку *formatter*.

### Задание 3
Конечно же ваша компания предоставляет примеры использования своих библиотек.
Чтобы продемонстрировать как работать с библиотекой *formatter_ex*,
вам необходимо создать два `CMakeList.txt` для двух простых приложений:
* *hello_world*, которое использует библиотеку *formatter_ex*;
* *solver*, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.

**Удачной стажировки!**

## Links
- [Основы сборки проектов на С/C++ при помощи CMake](https://eax.me/cmake/)
- [CMake Tutorial](http://neerc.ifmo.ru/wiki/index.php?title=CMake_Tutorial)
- [C++ Tutorial - make & CMake](https://www.bogotobogo.com/cplusplus/make.php)
- [Autotools](http://www.gnu.org/software/automake/manual/html_node/Autotools-Introduction.html)
- [CMake](https://cgold.readthedocs.io/en/latest/index.html)

```
Copyright (c) 2015-2021 The ISC Authors
```
