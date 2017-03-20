+++
tags = ["parser"]
topics = ["packages", "tools"]
description = "To read data files"
date = "2016-12-01T12:48:00+01:00"
title = "vle.reader"
+++

# Introduction <a name="Introduction"></a>

The vle package **vle.reader** provides functions for reading 2D table
matrices (eg. csv files). A data matrix can be filled using one call or
the file can be read line by line.


# Use case: read an entire file <a name="UseCase1"></a>

First, add your data file _data.txt_ into your package
(_mypackage/data/data.txt_). Then fill it with double, integers or strings.
In this example the first column contains double, the second contains integer,
and the third contains strings:
```
0.5 2 first_string
10.6 8 "second string"
```

Use the following code to parse this file and convert values
to vle::value::Value.

```
#include <vle/reader/table_file_reader.hpp>
#include <vle/utils/Package.hpp>

namespace vv = vle::value;
namespace vu = vle::utils;
namespace vr = vle::reader;
...
vv::Map params;                               //(1)
params.addString("sep"," ");                  //(2)
vv::Set& columns =  params.addSet("columns"); //(3)
columns.addString("double");                  //(4)
columns.addString("int");                     //(5)
columns.addString("string");                  //(6)
vu::Package pkg("mypackage");
vr::TableFileReader tfr(
  pkg.getDataFile("data.txt"),params);        //(7)
vv::Matrix mat;
tfr.readFile(mat);                            //(8)
std::cout << mat << std::endl;
```

The different steps of the above code do the following :
```
 (1) build a vle map that will contains parameters of the parser
 (2) set the type of separator between each column
 (3) add a set named 'columns' to the map. It wil contain the
            types of the columns.
 (4) add a column of type 'double'
 (5) add a column of type 'int'
 (6) add a column of type 'string'
 (7) instantiates a 'TableFileReader' with the parameters and the
  path to the 'data.txt' file, that we get using the vle::utils::Package API.
 (8) read the entire file using the function TableFileReader::readFile.
  This function takes a matrix as argument and will fill it with the data.
```

# Use case: read a file line by line <a name="UseCase2"></a>

To read the file line by line, use the function _readLine_.
Starting from the first use case, just replace step 8 by :

```
...
vv::Set set;
tfr.readLine(set);                        //(9)    
std::cout << set << std::endl;
tfr.readLine(set);                        //(10)    
std::cout << set << std::endl;
```
