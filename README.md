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




