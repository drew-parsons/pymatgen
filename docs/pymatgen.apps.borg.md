---
layout: default
title: pymatgen.apps.borg.md
nav_exclude: true
---

# pymatgen.apps.borg package

The borg package contains modules that assimilate large quantities of data into
pymatgen objects for analysis.

## Subpackages


* [pymatgen.apps.borg.tests package](pymatgen.apps.borg.tests.md)




    * [pymatgen.apps.borg.tests.test_hive module](pymatgen.apps.borg.tests.md#module-pymatgen.apps.borg.tests.test_hive)


        * [`GaussianToComputedEntryDroneTest`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.GaussianToComputedEntryDroneTest)


            * [`GaussianToComputedEntryDroneTest.setUp()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.GaussianToComputedEntryDroneTest.setUp)


            * [`GaussianToComputedEntryDroneTest.tearDown()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.GaussianToComputedEntryDroneTest.tearDown)


            * [`GaussianToComputedEntryDroneTest.test_assimilate()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.GaussianToComputedEntryDroneTest.test_assimilate)


            * [`GaussianToComputedEntryDroneTest.test_get_valid_paths()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.GaussianToComputedEntryDroneTest.test_get_valid_paths)


            * [`GaussianToComputedEntryDroneTest.test_to_from_dict()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.GaussianToComputedEntryDroneTest.test_to_from_dict)


        * [`SimpleVaspToComputedEntryDroneTest`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.SimpleVaspToComputedEntryDroneTest)


            * [`SimpleVaspToComputedEntryDroneTest.setUp()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.SimpleVaspToComputedEntryDroneTest.setUp)


            * [`SimpleVaspToComputedEntryDroneTest.tearDown()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.SimpleVaspToComputedEntryDroneTest.tearDown)


            * [`SimpleVaspToComputedEntryDroneTest.test_get_valid_paths()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.SimpleVaspToComputedEntryDroneTest.test_get_valid_paths)


            * [`SimpleVaspToComputedEntryDroneTest.test_to_from_dict()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.SimpleVaspToComputedEntryDroneTest.test_to_from_dict)


        * [`VaspToComputedEntryDroneTest`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.VaspToComputedEntryDroneTest)


            * [`VaspToComputedEntryDroneTest.setUp()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.VaspToComputedEntryDroneTest.setUp)


            * [`VaspToComputedEntryDroneTest.tearDown()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.VaspToComputedEntryDroneTest.tearDown)


            * [`VaspToComputedEntryDroneTest.test_assimilate()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.VaspToComputedEntryDroneTest.test_assimilate)


            * [`VaspToComputedEntryDroneTest.test_get_valid_paths()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.VaspToComputedEntryDroneTest.test_get_valid_paths)


            * [`VaspToComputedEntryDroneTest.test_to_from_dict()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_hive.VaspToComputedEntryDroneTest.test_to_from_dict)


    * [pymatgen.apps.borg.tests.test_queen module](pymatgen.apps.borg.tests.md#module-pymatgen.apps.borg.tests.test_queen)


        * [`BorgQueenTest`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_queen.BorgQueenTest)


            * [`BorgQueenTest.setUp()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_queen.BorgQueenTest.setUp)


            * [`BorgQueenTest.tearDown()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_queen.BorgQueenTest.tearDown)


            * [`BorgQueenTest.test_get_data()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_queen.BorgQueenTest.test_get_data)


            * [`BorgQueenTest.test_load_data()`](pymatgen.apps.borg.tests.md#pymatgen.apps.borg.tests.test_queen.BorgQueenTest.test_load_data)



## pymatgen.apps.borg.hive module

This module define the various drones used to assimilate data.


### _class_ pymatgen.apps.borg.hive.AbstractDrone()
Bases: `MSONable`

Abstract drone class that defines the various methods that must be
implemented by drones. Because of the quirky nature of Python”s
multiprocessing, the intermediate data representations has to be in the
form of python primitives. So all objects that drones work with must be
MSONable. All drones must also implement the standard MSONable as_dict() and
from_dict API.


#### _abstract_ assimilate(path)
Assimilate data in a directory path into a pymatgen object. Because of
the quirky nature of Python’s multiprocessing, the object must support
pymatgen’s as_dict() for parallel processing.


* **Parameters**

    **path** – directory path



* **Returns**

    An assimilated object



#### _abstract_ get_valid_paths(path)
Checks if path contains valid data for assimilation, and then returns
the valid paths. The paths returned can be a list of directory or file
paths, depending on what kind of data you are assimilating. For
example, if you are assimilating VASP runs, you are only interested in
directories containing vasprun.xml files. On the other hand, if you are
interested converting all POSCARs in a directory tree to CIFs for
example, you will want the file paths.


* **Parameters**

    **path** – input path as a tuple generated from os.walk, i.e.,
    (parent, subdirs, files).



* **Returns**

    List of valid dir/file paths for assimilation



### _class_ pymatgen.apps.borg.hive.GaussianToComputedEntryDrone(inc_structure=False, parameters=None, data=None, file_extensions=('.log',))
Bases: `AbstractDrone`

GaussianToEntryDrone assimilates directories containing Gaussian output to
ComputedEntry/ComputedStructureEntry objects. By default, it is assumed
that Gaussian output files have a “.log” extension.

**NOTE**: Like the GaussianOutput class, this is still in early beta.


* **Parameters**


    * **inc_structure** (*bool*) – Set to True if you want
    ComputedStructureEntries to be returned instead of
    ComputedEntries.


    * **parameters** (*list*) – Input parameters to include. It has to be one of
    the properties supported by the GaussianOutput object. See
    `pymatgen.io.gaussianio GaussianOutput`. The parameters
    have to be one of python’s primitive types, i.e., list, dict of
    strings and integers. If parameters is None, a default set of
    parameters will be set.


    * **data** (*list*) – Output data to include. Has to be one of the properties
    supported by the GaussianOutput object. The parameters have to
    be one of python’s primitive types, i.e. list, dict of strings
    and integers. If data is None, a default set will be set.


    * **file_extensions** (*list*) – File extensions to be considered as Gaussian output files.
    Defaults to just the typical “log” extension.



#### as_dict()
Returns: MSONable dict.


#### assimilate(path)
Assimilate data in a directory path into a ComputedEntry object.


* **Parameters**

    **path** – directory path



* **Returns**

    ComputedEntry



#### _classmethod_ from_dict(dct)

* **Parameters**

    **dct** (*dict*) – Dict Representation.



* **Returns**

    GaussianToComputedEntryDrone



#### get_valid_paths(path)
Checks if path contains files with define extensions.


* **Parameters**

    **path** – input path as a tuple generated from os.walk, i.e.,
    (parent, subdirs, files).



* **Returns**

    List of valid dir/file paths for assimilation



### _class_ pymatgen.apps.borg.hive.SimpleVaspToComputedEntryDrone(inc_structure=False)
Bases: `VaspToComputedEntryDrone`

A simpler VaspToComputedEntryDrone. Instead of parsing vasprun.xml, it
parses only the INCAR, POTCAR, OSZICAR and KPOINTS files, which are much
smaller and faster to parse. However, much fewer properties are available
compared to the standard VaspToComputedEntryDrone.


* **Parameters**

    **inc_structure** (*bool*) – Set to True if you want
    ComputedStructureEntries to be returned instead of
    ComputedEntries. Structure will be parsed from the CONTCAR.



#### as_dict()
Returns: MSONable dict.


#### assimilate(path)
Assimilate data in a directory path into a ComputedEntry object.


* **Parameters**

    **path** – directory path



* **Returns**

    ComputedEntry



#### _classmethod_ from_dict(dct)

* **Parameters**

    **dct** (*dict*) – Dict Representation.



* **Returns**

    SimpleVaspToComputedEntryDrone



### _class_ pymatgen.apps.borg.hive.VaspToComputedEntryDrone(inc_structure=False, parameters=None, data=None)
Bases: `AbstractDrone`

VaspToEntryDrone assimilates directories containing VASP output to
ComputedEntry/ComputedStructureEntry objects.

There are some restrictions on the valid directory structures:


1. There can be only one vasp run in each directory.


2. Directories designated “relax1”, “relax2” are considered to be 2 parts
of an aflow style run, and only “relax2” is parsed.


3. The drone parses only the vasprun.xml file.


* **Parameters**


    * **inc_structure** (*bool*) – Set to True if you want
    ComputedStructureEntries to be returned instead of
    ComputedEntries.


    * **parameters** (*list*) – Input parameters to include. It has to be one of
    the properties supported by the Vasprun object. See
    `pymatgen.io.vasp.Vasprun`. If parameters is None,
    a default set of parameters that are necessary for typical
    post-processing will be set.


    * **data** (*list*) – Output data to include. Has to be one of the properties
    supported by the Vasprun object.



#### as_dict()
Returns: MSONABle dict.


#### assimilate(path)
Assimilate data in a directory path into a ComputedEntry object.


* **Parameters**

    **path** – directory path



* **Returns**

    ComputedEntry



#### _classmethod_ from_dict(dct)

* **Parameters**

    **dct** (*dict*) – Dict Representation.



* **Returns**

    VaspToComputedEntryDrone



#### get_valid_paths(path)
Checks if paths contains vasprun.xml or (POSCAR+OSZICAR).


* **Parameters**

    **path** – input path as a tuple generated from os.walk, i.e.,
    (parent, subdirs, files).



* **Returns**

    List of valid dir/file paths for assimilation


## pymatgen.apps.borg.queen module

This module defines the BorgQueen class, which manages drones to assimilate
data using Python’s multiprocessing.


### _class_ pymatgen.apps.borg.queen.BorgQueen(drone, rootpath=None, number_of_drones=1)
Bases: `object`

The Borg Queen controls the drones to assimilate data in an entire
directory tree. Uses multiprocessing to speed up things considerably. It
also contains convenience methods to save and load data between sessions.


* **Parameters**


    * **drone** (*Drone*) – An implementation of
    `pymatgen.apps.borg.hive.AbstractDrone` to use for
    assimilation.


    * **rootpath** (*str*) – The root directory to start assimilation. Leave it
    as None if you want to do assimilation later, or is using the
    BorgQueen to load previously assimilated data.


    * **number_of_drones** (*int*) – Number of drones to parallelize over.
    Typical machines today have up to four processors. Note that you
    won’t see a 100% improvement with two drones over one, but you
    will definitely see a significant speedup of at least 50% or so.
    If you are running this over a server with far more processors,
    the speedup will be even greater.



#### get_data()
Returns an list of assimilated objects.


#### load_data(filename)
Load assimilated data from a file.


#### parallel_assimilate(rootpath)
Assimilate the entire subdirectory structure in rootpath.


#### save_data(filename)
Save the assimilated data to a file.


* **Parameters**

    **filename** (*str*) – filename to save the assimilated data to. Note
    that if the filename ends with gz or bz2, the relevant gzip
    or bz2 compression will be applied.



#### serial_assimilate(rootpath)
Assimilate the entire subdirectory structure in rootpath serially.


### pymatgen.apps.borg.queen.order_assimilation(args)
Internal helper method for BorgQueen to process assimilation.