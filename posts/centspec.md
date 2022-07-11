---
title: 'EPOCH Code For Spectrum'
date: '2022-06-30'
---

Use EPOCH Code to get axis spectrum

## SDF_Write

Use this syntex can save axis Ey to file:

```Fortran
CALL sdf_write_plain_variable(sdf_handle, id, name, 
units, dims, stagger, & grid_id, variable,
subtype_field, subarray_field)  
```

The parameters have the following types and meanings:

$\cdot$ block id - The id name of the variable. This character string is a unique identifier for the variable in the file enabling a program to retrieve it later. Once defined it should not change so that newer versions of EPOCH can still identify variables generated by older versions.

$\cdot$ name - The display name of the variable. This character string is the name that is used by external programs to display an identifying name for the variable. If it contains ’/’ characters then these are used by VisIt to group the variables.

$\cdot$ units - The units of the variable. This character string is used when displaying the data units. For most variables in EPOCH these are SI units.

$\cdot$ dims - An nD integer array containing the GLOBAL length of the variable across all processors. In EPOCH a variable actually called “dims” exists for variables which are the same size as the default field variables.

$\cdot$ stagger - An integer constant containing the stagger of a variable from the cell centre of a cell. This property lets external programs know the position of a variable on the grid.

$\cdot$ grid id - The id name of the grid to which the variable is attached. In EPOCH , the main grid is just called “grid”. Note that this property is case sensitive.

$\cdot$ variable - The actual variable to be written to disk.

$\cdot$ subtype field - This is an MPI type representing the layout of the data across the processors. For a standard field variable, there is an automatically created type called “subtype field” which should be used here.

$\cdot$ subarray field - This is an MPI type representing the section of the “variable” parameter to be written. For a standard field variable, there is an automatically created type called “subarray field” which should be used here.

## Example

For Example, derived variables **array**

```Fortran
IF (IAND(dumpmask(c_dump_myvar), code)) THEN
  CALL calc_my_variable(array)
  CALL sdf_write_plain_variable(sdf_handle, ’my_var’,
  ’Mine/variable’, ’unit’, dims, c_stagger_cell_centre, 
  ’grid’, array, subtype_field, subarray_field)
ENDIF
```

## Cent Spec

extract the central ey and save to sdf by subroutine **sdf_write_plain_variable(...)**