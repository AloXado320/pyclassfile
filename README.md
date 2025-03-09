pyclassfile
============
A modifed version of classfile that lazily adds extra attributes to fix output on some class files I'm analyzing for a tool.

ORIGINAL README
============

classfile.py
============

classfile.py is a java class file formatter / decompiler / compiler 
that transforms between binary java class files and a python object
graph (dicts and arrays).

classfile can be used as a python module or run as a script.

    usage:
      classfile.py -d <classfile>
      classfile.py -c <pyobjfile> <classfile>


Why
---
The JVM is a great piece of technology, but I prefer not to use the Java
language.  classfile.py makes it possible to view and manipulate class
files in python.

More Info
---------
Info about the java class file format at:

* http://java.sun.com/docs/books/jvms/second_edition/html/ClassFile.doc.html
* http://jcp.org/aboutJava/communityprocess/final/jsr202/index.html

Supported Features
------------------
Round tripping should work for any class file.
There are some class file attributes that are not yet supported, but
when these are encountered, the attributes are written in binary format
and can be read back from binary format.

Example
-------
[Here's an example](https://github.com/AloXado320/pyclassfile/blob/master/README.md) on how to use this script.
