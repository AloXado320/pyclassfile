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
Start with a Java source file or class file:

    public class Example {
        private static String foo = "world";
        public static void main(String[] args) {
            int times = 2;
            for (int i = 0; i < times; i++) {
                System.out.println("hello " + foo);
            }
        }
    }

Compile and Run:

    $ javac Example.java
    $ java Example
    hello world
    hello world

Now use classfile to decompile:

    $ ./classfile.py -d Example.class > Example.py

This will show the contents of the classfile as a python object:

    {'01_magic': 'cafebabe',
     '02_minor_version': 0,
     '03_major_version': 50,
     '04_constant_pool_count': 57,
     '05_cp_info': [{'00_index': 0,
                     '00_tag_name': 'unusable at start to get numbering working',
                     '01_tag': 0},
                    {'00_index': 1,
                     '00_tag_name': 'CONSTANT_Class',
                     '01_tag': 7,
                     '02_name_index': 2},
                    {'00_index': 2,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 7,
                     '03_bytes': 'Example'},
                    {'00_index': 3,
                     '00_tag_name': 'CONSTANT_Class',
                     '01_tag': 7,
                     '02_name_index': 4},
                    {'00_index': 4,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 16,
                     '03_bytes': 'java/lang/Object'},
                    {'00_index': 5,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 3,
                     '03_bytes': 'foo'},
                    {'00_index': 6,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 18,
                     '03_bytes': 'Ljava/lang/String;'},
                    {'00_index': 7,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 8,
                     '03_bytes': '<clinit>'},
                    {'00_index': 8,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 3,
                     '03_bytes': '()V'},
                    {'00_index': 9,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 4,
                     '03_bytes': 'Code'},
                    {'00_index': 10,
                     '00_tag_name': 'CONSTANT_String',
                     '00_value': 'world',
                     '01_tag': 8,
                     '02_string_index': 11},
                    {'00_index': 11,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 5,
                     '03_bytes': 'world'},
                    {'00_index': 12,
                     '00_tag_name': 'CONSTANT_Fieldref',
                     '01_tag': 9,
                     '02_class_index': 1,
                     '03_name_and_type_index': 13},
                    {'00_index': 13,
                     '00_tag_name': 'CONSTANT_NameAndType',
                     '01_tag': 12,
                     '02_name_index': 5,
                     '03_descriptor_index': 6},
                    {'00_index': 14,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 15,
                     '03_bytes': 'LineNumberTable'},
                    {'00_index': 15,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 18,
                     '03_bytes': 'LocalVariableTable'},
                    {'00_index': 16,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 6,
                     '03_bytes': '<init>'},
                    {'00_index': 17,
                     '00_tag_name': 'CONSTANT_Methodref',
                     '01_tag': 10,
                     '02_class_index': 3,
                     '03_name_and_type_index': 18},
                    {'00_index': 18,
                     '00_tag_name': 'CONSTANT_NameAndType',
                     '01_tag': 12,
                     '02_name_index': 16,
                     '03_descriptor_index': 8},
                    {'00_index': 19,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 4,
                     '03_bytes': 'this'},
                    {'00_index': 20,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 9,
                     '03_bytes': 'LExample;'},
                    {'00_index': 21,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 4,
                     '03_bytes': 'main'},
                    {'00_index': 22,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 22,
                     '03_bytes': '([Ljava/lang/String;)V'},
                    {'00_index': 23,
                     '00_tag_name': 'CONSTANT_Fieldref',
                     '01_tag': 9,
                     '02_class_index': 24,
                     '03_name_and_type_index': 26},
                    {'00_index': 24,
                     '00_tag_name': 'CONSTANT_Class',
                     '01_tag': 7,
                     '02_name_index': 25},
                    {'00_index': 25,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 16,
                     '03_bytes': 'java/lang/System'},
                    {'00_index': 26,
                     '00_tag_name': 'CONSTANT_NameAndType',
                     '01_tag': 12,
                     '02_name_index': 27,
                     '03_descriptor_index': 28},
                    {'00_index': 27,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 3,
                     '03_bytes': 'out'},
                    {'00_index': 28,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 21,
                     '03_bytes': 'Ljava/io/PrintStream;'},
                    {'00_index': 29,
                     '00_tag_name': 'CONSTANT_Class',
                     '01_tag': 7,
                     '02_name_index': 30},
                    {'00_index': 30,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 23,
                     '03_bytes': 'java/lang/StringBuilder'},
                    {'00_index': 31,
                     '00_tag_name': 'CONSTANT_String',
                     '00_value': 'hello ',
                     '01_tag': 8,
                     '02_string_index': 32},
                    {'00_index': 32,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 6,
                     '03_bytes': 'hello '},
                    {'00_index': 33,
                     '00_tag_name': 'CONSTANT_Methodref',
                     '01_tag': 10,
                     '02_class_index': 29,
                     '03_name_and_type_index': 34},
                    {'00_index': 34,
                     '00_tag_name': 'CONSTANT_NameAndType',
                     '01_tag': 12,
                     '02_name_index': 16,
                     '03_descriptor_index': 35},
                    {'00_index': 35,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 21,
                     '03_bytes': '(Ljava/lang/String;)V'},
                    {'00_index': 36,
                     '00_tag_name': 'CONSTANT_Methodref',
                     '01_tag': 10,
                     '02_class_index': 29,
                     '03_name_and_type_index': 37},
                    {'00_index': 37,
                     '00_tag_name': 'CONSTANT_NameAndType',
                     '01_tag': 12,
                     '02_name_index': 38,
                     '03_descriptor_index': 39},
                    {'00_index': 38,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 6,
                     '03_bytes': 'append'},
                    {'00_index': 39,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 45,
                     '03_bytes': '(Ljava/lang/String;)Ljava/lang/StringBuilder;'},
                    {'00_index': 40,
                     '00_tag_name': 'CONSTANT_Methodref',
                     '01_tag': 10,
                     '02_class_index': 29,
                     '03_name_and_type_index': 41},
                    {'00_index': 41,
                     '00_tag_name': 'CONSTANT_NameAndType',
                     '01_tag': 12,
                     '02_name_index': 42,
                     '03_descriptor_index': 43},
                    {'00_index': 42,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 8,
                     '03_bytes': 'toString'},
                    {'00_index': 43,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 20,
                     '03_bytes': '()Ljava/lang/String;'},
                    {'00_index': 44,
                     '00_tag_name': 'CONSTANT_Methodref',
                     '01_tag': 10,
                     '02_class_index': 45,
                     '03_name_and_type_index': 47},
                    {'00_index': 45,
                     '00_tag_name': 'CONSTANT_Class',
                     '01_tag': 7,
                     '02_name_index': 46},
                    {'00_index': 46,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 19,
                     '03_bytes': 'java/io/PrintStream'},
                    {'00_index': 47,
                     '00_tag_name': 'CONSTANT_NameAndType',
                     '01_tag': 12,
                     '02_name_index': 48,
                     '03_descriptor_index': 35},
                    {'00_index': 48,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 7,
                     '03_bytes': 'println'},
                    {'00_index': 49,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 4,
                     '03_bytes': 'args'},
                    {'00_index': 50,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 19,
                     '03_bytes': '[Ljava/lang/String;'},
                    {'00_index': 51,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 5,
                     '03_bytes': 'times'},
                    {'00_index': 52,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 1,
                     '03_bytes': 'I'},
                    {'00_index': 53,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 1,
                     '03_bytes': 'i'},
                    {'00_index': 54,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 13,
                     '03_bytes': 'StackMapTable'},
                    {'00_index': 55,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 10,
                     '03_bytes': 'SourceFile'},
                    {'00_index': 56,
                     '00_tag_name': 'CONSTANT_Utf8',
                     '01_tag': 1,
                     '02_length': 12,
                     '03_bytes': 'Example.java'}],
     '06_access_flags': 33,
     '07_this_class': 1,
     '08_super_class': 3,
     '09_interfaces_count': 0,
     '10_interfaces': (),
     '11_fields_count': 1,
     '12_field_info': [{'00_field_name': 'foo',
                        '01_access_flags': 10,
                        '02_name_index': 5,
                        '03_descriptor_index': 6,
                        '04_attributes_count': 0,
                        '05_attribute_info': []}],
     '13_methods_count': 3,
     '14_method_info': [{'00_method_name': '<clinit>()V',
                         '01_access_flags': 8,
                         '02_name_index': 7,
                         '03_descriptor_index': 8,
                         '04_attributes_count': 1,
                         '05_attribute_info': [{'00_attribute_name': 'Code',
                                                '01_attribute_name_index': 9,
                                                '02_attribute_length': 42,
                                                '03_max_stack': 1,
                                                '04_max_locals': 0,
                                                '05_code_length': 6,
                                                '06_code': ['   0:   2:ldc 10              #',
                                                            '   2:   ?:putstatic 12        # fooLjava/lang/String;',
                                                            '   5:   1:return              #'],
                                                '07_exception_table_length': 0,
                                                '08_exception_table': [],
                                                '09_attributes_count': 2,
                                                '10_attribute_info': [{'00_attribute_name': 'LineNumberTable',
                                                                       '01_attribute_name_index': 14,
                                                                       '02_attribute_length': 10,
                                                                       '03_line_number_table_length': 2,
                                                                       '04_line_number_table': [{'01_start_pc': 0,
                                                                                                 '02_line_number': 2},
                                                                                                {'01_start_pc': 5,
                                                                                                 '02_line_number': 1}]},
                                                                      {'00_attribute_name': 'LocalVariableTable',
                                                                       '01_attribute_name_index': 15,
                                                                       '02_attribute_length': 2,
                                                                       '03_local_variable_table_length': 0,
                                                                       '04_local_variable_table': []}]}]},
                        {'00_method_name': '<init>()V',
                         '01_access_flags': 1,
                         '02_name_index': 16,
                         '03_descriptor_index': 8,
                         '04_attributes_count': 1,
                         '05_attribute_info': [{'00_attribute_name': 'Code',
                                                '01_attribute_name_index': 9,
                                                '02_attribute_length': 47,
                                                '03_max_stack': 1,
                                                '04_max_locals': 1,
                                                '05_code_length': 5,
                                                '06_code': ['   0:   1:aload_0             #',
                                                            '   1:   ?:invokespecial 17    # <init>()V',
                                                            '   4:   ?:return              #'],
                                                '07_exception_table_length': 0,
                                                '08_exception_table': [],
                                                '09_attributes_count': 2,
                                                '10_attribute_info': [{'00_attribute_name': 'LineNumberTable',
                                                                       '01_attribute_name_index': 14,
                                                                       '02_attribute_length': 6,
                                                                       '03_line_number_table_length': 1,
                                                                       '04_line_number_table': [{'01_start_pc': 0,
                                                                                                 '02_line_number': 1}]},
                                                                      {'00_attribute_name': 'LocalVariableTable',
                                                                       '01_attribute_name_index': 15,
                                                                       '02_attribute_length': 12,
                                                                       '03_local_variable_table_length': 1,
                                                                       '04_local_variable_table': [{'00_name': 'LExample; this',
                                                                                                    '01_start_pc': 0,
                                                                                                    '02_length': 5,
                                                                                                    '03_name_index': 19,
                                                                                                    '04_descriptor_index': 20,
                                                                                                    '05_index': 0}]}]}]},
                        {'00_method_name': 'main([Ljava/lang/String;)V',
                         '01_access_flags': 9,
                         '02_name_index': 21,
                         '03_descriptor_index': 22,
                         '04_attributes_count': 1,
                         '05_attribute_info': [{'00_attribute_name': 'Code',
                                                '01_attribute_name_index': 9,
                                                '02_attribute_length': 132,
                                                '03_max_stack': 4,
                                                '04_max_locals': 3,
                                                '05_code_length': 40,
                                                '06_code': ['   0:   4:iconst_2            #',
                                                            '   1:   ?:istore_1            #',
                                                            '   2:   5:iconst_0            #',
                                                            '   3:   ?:istore_2            #',
                                                            '   4:   ?:goto 30             #',
                                                            '   7:   6:getstatic 23        # outLjava/io/PrintStream;',
                                                            '  10:   ?:new 29              # java/lang/StringBuilder',
                                                            '  13:   ?:dup                 #',
                                                            '  14:   ?:ldc 31              #',
                                                            '  16:   ?:invokespecial 33    # <init>(Ljava/lang/String;)V',
                                                            '  19:   ?:getstatic 12        # fooLjava/lang/String;',
                                                            '  22:   ?:invokevirtual 36    # append(Ljava/lang/String;)Ljava/lang/StringBuilder;',
                                                            '  25:   ?:invokevirtual 40    # toString()Ljava/lang/String;',
                                                            '  28:   ?:invokevirtual 44    # println(Ljava/lang/String;)V',
                                                            '  31:   5:iinc 2 1            #',
                                                            '  34:   ?:iload_2             #',
                                                            '  35:   ?:iload_1             #',
                                                            '  36:   ?:if_icmplt -29       #',
                                                            '  39:   8:return              #'],
                                                '07_exception_table_length': 0,
                                                '08_exception_table': [],
                                                '09_attributes_count': 3,
                                                '10_attribute_info': [{'00_attribute_name': 'LineNumberTable',
                                                                       '01_attribute_name_index': 14,
                                                                       '02_attribute_length': 22,
                                                                       '03_line_number_table_length': 5,
                                                                       '04_line_number_table': [{'01_start_pc': 0,
                                                                                                 '02_line_number': 4},
                                                                                                {'01_start_pc': 2,
                                                                                                 '02_line_number': 5},
                                                                                                {'01_start_pc': 7,
                                                                                                 '02_line_number': 6},
                                                                                                {'01_start_pc': 31,
                                                                                                 '02_line_number': 5},
                                                                                                {'01_start_pc': 39,
                                                                                                 '02_line_number': 8}]},
                                                                      {'00_attribute_name': 'LocalVariableTable',
                                                                       '01_attribute_name_index': 15,
                                                                       '02_attribute_length': 32,
                                                                       '03_local_variable_table_length': 3,
                                                                       '04_local_variable_table': [{'00_name': '[Ljava/lang/String; args',
                                                                                                    '01_start_pc': 0,
                                                                                                    '02_length': 40,
                                                                                                    '03_name_index': 49,
                                                                                                    '04_descriptor_index': 50,
                                                                                                    '05_index': 0},
                                                                                                   {'00_name': 'I times',
                                                                                                    '01_start_pc': 2,
                                                                                                    '02_length': 38,
                                                                                                    '03_name_index': 51,
                                                                                                    '04_descriptor_index': 52,
                                                                                                    '05_index': 1},
                                                                                                   {'00_name': 'I i',
                                                                                                    '01_start_pc': 4,
                                                                                                    '02_length': 35,
                                                                                                    '03_name_index': 53,
                                                                                                    '04_descriptor_index': 52,
                                                                                                    '05_index': 2}]},
                                                                      {'00_attribute_name': 'StackMapTable',
                                                                       '01_attribute_name_index': 54,
                                                                       '02_attribute_length': 8,
                                                                       '03_info': '\x00\x02\xfd\x00\x07\x01\x01\x1a'}]}]}],
     '15_attributes_count': 1,
     '16_attribute_info': [{'00_attribute_name': 'SourceFile',
                            '00_sourcefile': 'Example.java',
                            '01_attribute_name_index': 55,
                            '02_attribute_length': 2,
                            '03_sourcefile_index': 56}]}

                        
This can be modified by using a text editor, or by using python code
and then converted back to a class file.

This python code will decompile, modify the code to print 'hello world' 3 times, then write
back the classfile.


    import classfile
    cf = classfile.decompile(open('Example.class').read())
    m = [m for m in cf['14_method_info'] if m['00_method_name'].startswith('main')][0]
    c = [a for a in m['05_attribute_info'] if a['00_attribute_name'] == 'Code'][0]['06_code']
    c[0] = c[0].replace('iconst_2', 'iconst_3')
    classfile.compile(cf, 'Example.class')

Now when we run the class:

    $ java Example
    hello world
    hello world
    hello world
