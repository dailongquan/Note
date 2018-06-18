# cmake-variables


## CMAKE_PREFIX_PATH

Path used for searching by FIND_XXX(), with appropriate suffixes added.

Specifies a path which will be used by the FIND_XXX() commands. It contains the “base” directories, the FIND_XXX() commands append appropriate subdirectories to the base directories. So FIND_PROGRAM() adds /bin to each of the directories in the path, FIND_LIBRARY() appends /lib to each of the directories, and FIND_PATH() and FIND_FILE() append /include . By default it is empty, it is intended to be set by the project. See also CMAKE_SYSTEM_PREFIX_PATH, CMAKE_INCLUDE_PATH, CMAKE_LIBRARY_PATH, CMAKE_PROGRAM_PATH.

## CMAKE_INCLUDE_PATH

Path used for searching by FIND_FILE() and FIND_PATH().

Specifies a path which will be used both by FIND_FILE() and FIND_PATH(). Both commands will check each of the contained directories for the existence of the file which is currently searched. By default it is empty, it is intended to be set by the project. See also CMAKE_SYSTEM_INCLUDE_PATH, CMAKE_PREFIX_PATH.

## CMAKE_LIBRARY_PATH

Path used for searching by FIND_LIBRARY().

Specifies a path which will be used by FIND_LIBRARY(). FIND_LIBRARY() will check each of the contained directories for the existence of the library which is currently searched. By default it is empty, it is intended to be set by the project. See also CMAKE_SYSTEM_LIBRARY_PATH, CMAKE_PREFIX_PATH.

## CMAKE_PROGRAM_PATH

Path used for searching by FIND_PROGRAM().

Specifies a path which will be used by FIND_PROGRAM(). FIND_PROGRAM() will check each of the contained directories for the existence of the program which is currently searched. By default it is empty, it is intended to be set by the project. See also CMAKE_SYSTEM_PROGRAM_PATH, CMAKE_PREFIX_PATH.

## CMAKE_SYSTEM_PREFIX_PATH

;-list of directories specifying installation prefixes to be searched by the find_package(), find_program(), find_library(), find_file(), and find_path() commands. Each command will add appropriate subdirectories (like bin, lib, or include) as specified in its own documentation.

By default this contains the standard directories for the current system, the CMAKE_INSTALL_PREFIX, and the CMAKE_STAGING_PREFIX. The installation and staging prefixes may be excluded by setting the CMAKE_FIND_NO_INSTALL_PREFIX variable.

CMAKE_SYSTEM_PREFIX_PATH is not intended to be modified by the project; use CMAKE_PREFIX_PATH for this.

See also CMAKE_SYSTEM_INCLUDE_PATH, CMAKE_SYSTEM_LIBRARY_PATH, CMAKE_SYSTEM_PROGRAM_PATH, and CMAKE_SYSTEM_IGNORE_PATH.


## CMAKE_SYSTEM_INCLUDE_PATH

;-list of directories specifying a search path for the find_file() and find_path() commands. By default this contains the standard directories for the current system. It is not intended to be modified by the project; use CMAKE_INCLUDE_PATH for this. See also CMAKE_SYSTEM_PREFIX_PATH.


## CMAKE_SYSTEM_LIBRARY_PATH

;-list of directories specifying a search path for the find_library() command. By default this contains the standard directories for the current system. It is not intended to be modified by the project; use CMAKE_LIBRARY_PATH for this. See also CMAKE_SYSTEM_PREFIX_PATH.

## CMAKE_SYSTEM_PROGRAM_PATH

;-list of directories specifying a search path for the find_program() command. By default this contains the standard directories for the current system. It is not intended to be modified by the project; use CMAKE_PROGRAM_PATH for this. See also CMAKE_SYSTEM_PREFIX_PATH.

## CMAKE_SYSTEM_IGNORE_PATH

;-list of directories to be ignored by the find_program(), find_library(), find_file(), and find_path() commands. This is useful in cross-compiling environments where some system directories contain incompatible but possibly linkable libraries. For example, on cross-compiled cluster environments, this allows a user to ignore directories containing libraries meant for the front-end machine.

By default this contains a list of directories containing incompatible binaries for the host system. See the CMAKE_IGNORE_PATH variable that is intended to be set by the project.

See also the CMAKE_SYSTEM_PREFIX_PATH, CMAKE_SYSTEM_LIBRARY_PATH, CMAKE_SYSTEM_INCLUDE_PATH, and CMAKE_SYSTEM_PROGRAM_PATH variables.


#  cmake-commands

