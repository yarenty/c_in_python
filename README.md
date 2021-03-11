# Use C in python


## STEPS

### 0. Install swig

On mac:

```shell
brew install swig
```


### 1. Example C code is in example.c file ;-)

There are few functions and some veriable.

@TODO: Check with classes and more complex structures.


### 2. Creaate interface file *i* - example.i

Few questions waiting answers:

- why there is "%module" what is meaning
- what is between %{} 
- why there is copy what is inside braces also outside it -  without "extern"

### 3. Create python module by SWIG

It uses example interface:
```shell
swig -python example.i
```

### 4. Compile all 

```shell
gcc -c example.c example_wrap.c \
-I/usr/local/include/python2.8
```

or in mac after update to latest python (brew install python)
```shell
 gcc -c example.c example_wrap.c \                                                                                                                                                                                  (main*) 18:31:53
    -I/usr/local/Cellar/python@3.9/3.9.2_1/Frameworks/Python.framework/Versions/3.9/include/python3.9/
```

this will create 2 o files:
 - example.o
 - example_wrap.o

### 5. Linking - NOT WORKING!

```shell
ld -shared example.o example_wrap.o -o _example.so
```
```shell
ld -dynamiclib example.o example_wrap.o -o _example.so
```
```shell
gcc -bundle `python-config --ldflags` example.o example_wrap.o -o _example.so
```



```shell
 g++  -lpython -dylib example.o example_wrap.o -o _example.so  
```

```text
[/o/w/c_in_python] : g++  -lpython -dylib example.o example_wrap.o -o _example.so                                                                                                                                                       (main*) 19:02:36
Undefined symbols for architecture x86_64:
  "_PyCMethod_New", referenced from:
      SWIG_PyInstanceMethod_New(_object*, _object*) in example_wrap.o
  "_PyInstanceMethod_New", referenced from:
      SWIG_PyInstanceMethod_New(_object*, _object*) in example_wrap.o
  "_PyModule_Create2", referenced from:
      _PyInit__example in example_wrap.o
  "_PyUnicode_Concat", referenced from:
      SwigPyObject_repr(SwigPyObject*) in example_wrap.o
      swig_varlink_str(swig_varlinkobject*) in example_wrap.o
  "_PyUnicode_DecodeUTF8", referenced from:
      _wrap_get_time(_object*, _object*) in example_wrap.o
  "_PyUnicode_FromFormat", referenced from:
      SwigPyPacked_repr(SwigPyPacked*) in example_wrap.o
      SwigPyPacked_str(SwigPyPacked*) in example_wrap.o
      SwigPyObject_repr(SwigPyObject*) in example_wrap.o
  "_PyUnicode_FromString", referenced from:
      _PyInit__example in example_wrap.o
      _wrap_get_time(_object*, _object*) in example_wrap.o
      SWIG_Python_NewPointerObj(_object*, void*, swig_type_info*, int) in example_wrap.o
      SwigPyPacked_str(SwigPyPacked*) in example_wrap.o
      SWIG_Python_DestroyModule(_object*) in example_wrap.o
      swig_varlink_str(swig_varlinkobject*) in example_wrap.o
  "_PyUnicode_InternFromString", referenced from:
      swig_varlink_repr(swig_varlinkobject*) in example_wrap.o
      swig_varlink_str(swig_varlinkobject*) in example_wrap.o
  "__Py_Dealloc", referenced from:
      _PyInit__example in example_wrap.o
      _wrap_get_time(_object*, _object*) in example_wrap.o
      SWIG_Python_NewPointerObj(_object*, void*, swig_type_info*, int) in example_wrap.o
      SwigPyObject_dealloc(_object*) in example_wrap.o
      SWIG_Python_DestroyModule(_object*) in example_wrap.o
  "fact(int)", referenced from:
      _wrap_fact(_object*, _object*) in example_wrap.o
  "my_mod(int, int)", referenced from:
      _wrap_my_mod(_object*, _object*) in example_wrap.o
  "get_time()", referenced from:
      _wrap_get_time(_object*, _object*) in example_wrap.o
  "_main", referenced from:
     implicit entry/start for main executable
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

Tried with swig -c++ -python and using cxx files ... no luck
