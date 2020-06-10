Лабораторная работа №1 по ТиМП

Работу выполнил: Сакулин Даниил

1. Скачивание актуальной версии библиотеки Boost:

```
$ wget https://sourceforge.net/projects/boost/1.69.0/boost_1_69_0.tar.gz
```

2. Разархивирование библиотеки и удаление файла-архива:

```
$ tar -xf boost_1_69_0.tar.gz && rm boost_1_69_0.tar.gz
```

Проверка содержимого текущего каталога:

```
$ ls
boost_1_69_0
```

Переход в разархивированную директорию:

```
$ cd boost_1_69_0/
```

3. Подсчёт количества файлов в текущей директории:

```
$ ls -qp | grep -v / | wc -l
13
```
•	Получение списка файлов (-q - замена спец. символов на знак вопроса, -p - отображение суффиксов названий)

•	Исключение файлов, оканчивающихся на / (директорий)

•	Получение количества строк (кол-во файлов)

4.Подсчёт количества файлов во всей директории, включая вложенные:

```
$ find . -type f | wc –l
122382
```

5. Подсчёт количества файлов с расширением:

•	h либо hpp:

```
$ find . -type f -name '*.h' -o -name '*.hpp' | wc -l
30418
```

•	cpp:

```
$ find . -type f -name '*.cpp' | wc -l
27548
```

•	любым другим:

```
$ find . -type f ! -name '*.h' ! -name '*.hpp' ! -name '*cpp' | wc -l
64418
```

6. Нахождение полного пути до файла any.hpp:

```
$ realpath any.hpp
/home/yrojiobwuha/boost_1_69_0/any.hpp
```

7. Выведение списка файлов, упоминающих boost::asio:

```
$ grep -rl 'boost::asio' .
…
boost_1_69_0/libs/asio/example/cpp03/iostreams/http_client.cpp
boost_1_69_0/libs/asio/example/cpp03/iostreams/daytime_server.cpp
boost_1_69_0/libs/asio/example/cpp03/chat/chat_client.cpp
…
libs/process/test/exit_code.cpp
libs/process/test/async_pipe.cpp
libs/process/test/bind_stdin.cpp
```

8. Сборка boost:

```$ ./bootstrap.sh
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
Detecting Python version… 2.7
Detection Python root… /usr
Unicode/ICU support for Boost.Regex?... not found.
Generating Boost.Build configuration in project-config.jam...

Bootstrapping is done. To build, run:
    ./b2

To adjust configuration, edit 'project-config.jam'.
Further information:

   - Command line help:
     ./b2 --help

   - Getting started guide: 
     http://www.boost.org/more/getting_started/unix-variants.html

   - Boost.Build documentation:
     http://www.boost.org/build/doc/html/index.html
$ ./b2
Performing configuration checks

    - default address-model    : 64-bit
    - default architecture     : x86

Building the Boost C++ Libraries.
…
The Boost C++ Libraries were successfully built!

The following directory should be added to compiler include paths:
    /home/yrojiobwuha//boost_1_72_0

The following directory should be added to linker library paths:
    /home/ yrojiobwuha /boost_1_72_0/stage/lib
```

9. Перемещение собраной библиотеки в ~/boost-libs/ и перемещение в эту директорию:

```
$ mv ./stage/lib/ ~/boost-libs && cd ~/boost-libs/
```

10. Подсчёт размера каждого файла в дирректории:

```
$ du -b .
13088	./cmake/boost_iostreams-1.72.0
5864	./cmake/boost_headers-1.72.0
8841	./cmake/boost_stacktrace_windbg_cached-1.72.0
13557	./cmake/boost_stacktrace_basic-1.72.0
13331	./cmake/boost_type_erasure-1.72.0
…
13088	./cmake/boost_container-1.72.0
13758	./cmake/boost_unit_test_framework-1.72.0
12901	./cmake/boost_random-1.72.0
8407	./cmake/boost_fiber_numa-1.72.0
560589	./cmake
59161010	.
 $ wc -c `find . -type f`
   479528 ./libboost_serialization.so.1.72.0
  1440328 ./libboost_log.so.1.72.0
    15688 ./libboost_system.so.1.72.0
   110968 ./libboost_container.so.1.72.0
   807304 ./libboost_wserialization.a
…
   244104 ./libboost_thread.so.1.72.0
  1240230 ./libboost_serialization.a
   464664 ./libboost_math_tr1f.so.1.72.0
    16208 ./libboost_stacktrace_noop.so.1.72.0
  4489508 ./libboost_wave.a
 58957219 total
 ```
11. Выведение 10 файлов, занимающих наибольшее дисковое пространство:

```
 $ wc -c `find . -type f` | head -n -1 | sort -nr | head -n 10
  4674948 ./libboost_log.a
  4489508 ./libboost_wave.a
  3897354 ./libboost_math_tr1.a
  3876194 ./libboost_math_tr1f.a
  3865164 ./libboost_math_tr1l.a
  2914196 ./libboost_log_setup.a
  2887398 ./libboost_regex.a
  2489674 ./libboost_test_exec_monitor.a
  2470850 ./libboost_unit_test_framework.a
  2157000 ./libboost_locale.a
```
•	Подсчёт размера каждого файла (см. предыдущий пункт)

•	Игнорирование последней строчки (содержащей суммарный размер)

•	Сортировка, в соответствии с числовым значением

•	Получение последних 10 элементов списка (наибольших)

•	Разворот списка (от большего к меньшему)

