---
layout: post
title: "Thanks to CMake..."
date: 2019-08-15
htmlwidgets: true
author: RogerSGarcia
revised: true
image: "/images/p_cmake.png"
last_updated: 2019-08-19

---


{% include thankstocmake_graph.html %}

<center>
<widgetcaption>(Source: Google Trends <a href="https://trends.google.com/trends/explore?date=all&q=cmake,autoconf,scons,automake,qmake">Data</a>)</widgetcaption>
</center>

<hr/>

<h3>Less from Make (Makefiles) </h3>
Cmake was created in an effort to reduce the laborious effort that goes into writing lines of code for Makefiles. It's perhaps not evident until working with larger projects, but it's always valuable to work through a <code>Hello World</code>.

<hr/>

<h4>C++ <code>Hello World</code></h4>

<p>Let's get some info on our compiler.</p>
<p> More info on <a href="https://gcc.gnu.org/gcc-7/">GCC 7 release series</a> or use an <a href="https://www.onlinegdb.com/online_c++_compiler" class="btn btn-info" role="button">Online Compiler </a>
</p>

<pre class="sample"><code>$ g++ --version
g++ (Ubuntu 7.4.0-1ubuntu1~18.04.1) 7.4.0
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

</code></pre>

<p>Clone supporting repo for this tidbit</p>

<pre class="sample"><code>$ git clone https://github.com/RogerSGarcia/thankstocmake.git
Cloning into 'thankstocmake'...
remote: Enumerating objects: 11, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 11 (delta 0), reused 8 (delta 0), pack-reused 0
Unpacking objects: 100% (11/11), done.
$ ls
<span class="dirtext">thankstocmake</span>
$ cd thankstocmake/; ls
<span class="dirtext">helloworld</span>  <span class="dirtext">helloworld_cmake</span>  <span class="dirtext">helloworld_make</span>  README.md
</code></pre>

<p>Compile program using the command line</p>


<pre class="sample"><code>$ cd helloworld; ls
  helloworld.cpp
$ g++ helloworld.cpp -o hello.out
$ ls
  <span class="exetext">hello.out</span> helloworld.cpp
$ ./hello.out
Hello World
</code></pre>

<p>Compile program using a <code>Makefile</code></p>

<pre class="sample"><code>$ cd ../helloworld_make/
$ ls
helloworld.cpp Makefile
$ make
g++ helloworld.cpp -o hello.out
$ ls
  <span class="exetext">hello.out</span> helloworld.cpp Makefile
$ ./hello.out
Hello World
$ make clean
rm hello.out
</code></pre>

<p>Compile program using <code>cmake</code>. In general, you have a <code>CMakeLists.txt</code> file which contains commands that will generate our <code>Makefile</code>, this then allows us to invoke <code>make</code> like in the previous example (Awesome).</p>

<p>This may be old news to you if your frequently working with code, in particuarly C/C++, but it's pretty cool, despite different git-repositories/projects/libraries/ there's a common practice where source files are located and how you build your project using <code>cmake</code>:</p>

<dl class="row">
    <dt class="col-sm-3">src</dt>
    <dd class="col-sm-9">directory where source code is located.</dd>
    <dt class="col-sm-3 text-truncate">build</dt>
    <dd class="col-sm-9">directory you create with <code>mkdir</code> command and then run the command "<code>cmake ..</code>", you may find that a project (or yours) use different modes: <br> <code>Release</code> for an optimization build or a <code>Debug</code> mode for making your life easier when debugging (using <code>gdb</code>), so basically you can create a two directories for each mode: <code>build-release</code> directory and <code>build-debug</code></dd>
</dl>


<pre class="sample"><code>$ cd ../helloworld_cmake/
$ ls
  CMakeLists.txt <span class="dirtext">src</span>
$ mkdir build
$ cd build/
$ cmake ..
-- The C compiler identification is GNU 7.4.0
-- The CXX compiler identification is GNU 7.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/roger/ws/garcroge/tidbits_repo/thankstocmake/helloworld_cmake/build
$ ls
  CMakeCache.txt  <span class="dirtext">CMakeFiles</span>  cmake_install.cmake  Makefile
$ make -j8
<span class="scantext">Scanning dependencies of target hello.out</span>
[ 50%] <span class="yellowtext">Building CXX object CMakeFiles/hello.out.dir/src/helloworld.cpp.o</span>
[100%] <span class="exetext">Linking CXX executable hello.out</span>
[100%] Built target hello.out
$ ./hello.out
Hello World
</code></pre>


<p>Basically, CMake faciliates building Makefiles, but you will still need to invoke <code>Make</code> in order to call the compiler from the Makefile that contains bunch of flags and source files.</p>

<table class="table table-hover">
  <thead class="thead-light">
        <tr>
            <th>CMake</th>
            <th>Make (Makefile)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>generator of buildsystems</td>
            <td>a buildsystem</td>
        </tr>
        <tr>
            <td>projects/packages</td>
            <td>...</td>
        </tr>
        <tr>
            <td>guess compiler and flags</td>
            <td>make sure you indent</td>
        </tr>
        <tr>
            <td>full scripting, globbing, and a cache</td>
            <td>good luck</td>
        </tr>
        <tr>
            <td>fewer lines of code</td>
            <td>lines of code</td>
        </tr>
    </tbody>
</table>
