:py:mod:`usb.libloader`
=======================

.. py:module:: usb.libloader


Module Contents
---------------


Functions
~~~~~~~~~

- usb.libloader.locate_library
- usb.libloader.load_library
- usb.libloader.load_locate_library



.. py:exception:: LibraryException

   Bases: :py:obj:`OSError`

   Base class for I/O related errors.


.. py:exception:: LibraryNotFoundException

   Bases: :py:obj:`LibraryException`

   Base class for I/O related errors.


.. py:exception:: NoLibraryCandidatesException

   Bases: :py:obj:`LibraryNotFoundException`

   Base class for I/O related errors.


.. py:exception:: LibraryNotLoadedException

   Bases: :py:obj:`LibraryException`

   Base class for I/O related errors.


.. py:exception:: LibraryMissingSymbolsException

   Bases: :py:obj:`LibraryException`

   Base class for I/O related errors.


.. py:function:: locate_library(candidates, find_library=ctypes.util.find_library)

   Tries to locate a library listed in candidates using the given
   find_library() function (or ctypes.util.find_library).
   Returns the first library found, which can be the library's name
   or the path to the library file, depending on find_library().
   Returns None if no library is found.

   :param candidates: iterable with library names
   :param find_library: function that takes one positional arg (candidate)
			and returns a non-empty str if a library has been found.
			Any "false" value (None,False,empty str) is interpreted
			as "library not found".
			Defaults to ctypes.util.find_library if not given or
			None.


.. py:function:: load_library(lib, name=None, lib_cls=None)

   Loads a library. Catches and logs exceptions.

   :return: the loaded library or None

   :param lib: path to/name of the library to be loaded
   :param name: the library's identifier (for logging)
                Defaults to None.
   :param lib_cls: library class. Defaults to None (-> ctypes.CDLL).


.. py:function:: load_locate_library(candidates, cygwin_lib, name, win_cls=None, cygwin_cls=None, others_cls=None, find_library=None, check_symbols=None)

   Locates and loads a library.

   :return: the loaded library

   :param candidates: candidates list for locate_library()
   :param cygwin_lib: name of the cygwin library
   :param name: lib identifier (for logging). Defaults to None.
   :param win_cls: class that is used to instantiate the library on
                   win32 platforms. Defaults to None (-> ctypes.CDLL).
   :param cygwin_cls: library class for cygwin platforms.
                      Defaults to None (-> ctypes.CDLL).
   :param others_cls: library class for all other platforms.
                      Defaults to None (-> ctypes.CDLL).
   :param find_library: see locate_library(). Defaults to None.
   :check_symbols: either None or a list of symbols that the loaded lib
                   must provide (hasattr(<>)) in order to be considered
                   valid. LibraryMissingSymbolsException is raised if
                   any symbol is missing.

   :raises: NoLibraryCandidatesException
   :raises: LibraryNotFoundException
   :raises: LibraryNotLoadedException
   :raises: LibraryMissingSymbolsException
