.. _coding-standard:

Coding Standard
===============

Formatting
----------

Please be strict to the `Google C++ Style-Guide <https://google.github.io/styleguide/cppguide.html>`_. 
For ROS-specific naming, use the `ROS C++ Style-Guide <http://www.ros.org/wiki/CppStyleGuide>`_. 

.. raw:: html

  <details>
  <summary>Here is a guide on how to set up auto-formatting in your IDE with clang.</summary>

`Clang-Format <https://clang.llvm.org/docs/ClangFormat.html>`_ is a popular code formatting tool that helps maintain common code style across team members and IDEs. 
It provides an option to store formatting settings in special YAML files named .clang-format or _clang-format.

Installation
^^^^^^^^^^^^

.. code-block:: bash

  sudo apt install clang-format

Usage
^^^^^

Clang-Format searches for the nearest config file in the parent directories. 
Ideally, place the config file in the root directory of your repository. 
If you want to create a new config file from an existing style guide (for example google), use this command:

.. code-block:: bash
  
  clang-format -style=google -dump-config > .clang-format

After that, you probably want to format all the files in your repository:

.. code-block:: bash

  find . -regex '.*\.\(cpp\|hpp\|cc\|cxx\|h\)' -exec clang-format -style=file -i {} \;

IDE Integration
^^^^^^^^^^^^^^^

* In VS Code, install the extension ``xaver.clang-format``. 

* For CLion, follow `this guide <https://www.jetbrains.com/help/clion/clangformat-as-alternative-formatter.html>`_.


.. raw:: html

  </details>
  <br>

Exceptions to the ROS and Google Styles
---------------------------------------

* Use **80 columns**. 
  This is easier to navigate in GitHub and easier to read.

  .. raw:: html

    <details>
    <summary>If you are using the vs-code formatter, adapt it accordingly.</summary>

  .. code-block::

    {
      "cmake.configureOnOpen": false,
      "testMate.cpp.log.userId": "94452d06c5f1537839eb75b1160e000c2a49fe05",
      "C_Cpp.clang_format_path": "/usr/lib/llvm-6.0/bin/clang-format",
      "C_Cpp.clang_format_style": "file",
      "C_Cpp.clang_format_fallbackStyle": "none",
      "editor.formatOnSave": true,
      "testMate.cpp.log.logSentry": "disable_3",
      "editor.fontSize": 12,
      "terminal.integrated.shell.linux": "/bin/bash",
      // "C_Cpp.updateChannel": "Insiders",
      "editor.tabSize": 2,
      "window.zoomLevel": 1,
      "workbench.statusBar.visible": true,
      "window.menuBarVisibility": "toggle",
      "workbench.activityBar.visible": true,
      "editor.minimap.enabled": false,
      "workbench.sideBar.location": "left",
      "[cpp]": {
          "editor.defaultFormatter": "ms-vscode.cpptools"
      },
      "C_Cpp.updateChannel": "Insiders",
    }

  .. raw:: html

    </details>
    <br>


* Use #pragma once at the top of the header instead of include guards (#ifndef). 
  Although pragma once is not defined in the C++ standard, it is a widely supported preprocessor directive that is easier to use.

* Don't waste time on Doxygen. 
  The code should be for the most part self-explanatory. 
  Use simple comments with proper English grammar and punctuation for cases where the code is not straightforward to understand. 
  See `google style guide <https://google.github.io/styleguide/cppguide.html#Comments>`_.

* Don't use preprocessor directives at all (except pragma once). 
  Make your code configurable at run-time instead (gflags or ROS params). 
  Exceptions can be high-frequency code or architecture distinction. 
  Whenever possible, don't have preprocessor directives in headers.

* Use neither exceptions nor assertions. 
  Use glog checks instead. You may use assertions in VERY high frequency code.

* Use enum \class instead of enum whenever possible.

* Use of forward declarations is encouraged.

* Whenever possible, put includes in the cpp, not in the header.
  This reduces compilation time.

* Naming convention cheat-sheet: ClassName, variable_name, \class_member_variable_, functionName(), kCompileTimeConstant, MACROS.

* When implementing a virtual function from the base class, add override at the end of the function declaration for clarity. 
  Group these overrides together.

Additional Style Guidelines
---------------------------

* Suffix any physical size with its unit, e.g. ``time_s``, ``distance_m`` etc. 
  You can only leave out units if it's really, really obvious to everybody what unit is used, such as in accelerations or poses. 
  Only SI units and combinations thereof can ever be obvious.

* Put includes and dependencies in alphabetical ordering.

* Organize includes into blocks as follows:
  
  * Three blocks separated by empty lines:
    
    1. System/non-catkin-package includes with <>
    
    2. Includes from other catkin packages with <>
    
    3. Includes from the same package with ""

  * No additional empty lines

  * Each block arranged alphabetically

  * ``.cpp`` files have an additional first block for only the corresponding header with ""

    .. code-block:: C++

      #include "corresponding_header.h"

      #include <non-package dependency 1>
      #include <non-package dependency 2>
      ...

      #include <dependency from other package 1>
      #include <dependency from other package 2>
      ...

      #include "dependency from same package 1"
      #include "dependency from same package 2"
      ...

* Pass non-primitive types by const reference. 
  Don't return non-primitive types, use `output parameters <http://wiki.ros.org/CppStyleGuide#Output_arguments>`_ instead (acceptable exceptions: poses, positions, inline functions). 
  Make things const as much as possible. Only mutexes may be mutable.

* Don't use member variables of classes to store intermediate steps of functions that are not explicitly for modifying the class. 
  This obfuscates the data flow and makes it harder to understand the code.

* Try to keep your classes as ROS-agnostic as possible. 
  Ideally, all your subscribers should be managed in main(). 
  For publishers, this cannot always be done comfortably, but try to keep them at as high a level as possible.

* A header function class_name.h should only contain the class ClassName, and nothing else! 
  If you intend to put several free functions into a header, wrap them in a namespace which corresponds to the header name.