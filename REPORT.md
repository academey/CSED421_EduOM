# EduOM Report

Name: Park hyun joon

Student id: 20150968

# Problem Analysis

Operations for a structure related to a slotted page for storing an object have been implemented. CatOverlay, a data structure for storing information about data files, had to be used. 

# Design For Problem Solving
I tried to solve the problem with the appropriate size using the available space list.

## High Level

In order to make the most of the given variables, I tried to find libraries in the code as much as possible. In addition, pages and catalogs were written with consideration about how to inquire as little as possible to reduce I/O.

## Low Level

Syntax such as Early Return was used to increase the readability of the code.

# Mapping Between Implementation And the Design

FILL WITH YOUR CODE IMPLEMENTATION DESCRIPTION

- EduOM_CompactPage
Fill in the original page using the stored page object for each non-empty slot. If a specific slotNo exists, only the corresponding object is last saved again.

- EduOM_CreateObject
A function that generates an object. Create a new object and initialize it. Delegate the detailed implementation to eduom_createobject.

- eduom_CreateObject
After importing the catalog object of the data file, replace the firstPage and volNo of the data file catalog information with the physicalFileId. And determine whether nearObj is NULL or not. If NULL, use sm_CatOverlayForData to search for availSpaceList. Then select the appropriate page. If it is not NULL, you can set it to the same page as nearObj. And if you have finished setting the page, you can insert the object into the area.

- EduOM_DestroyObject
It is a function that removes an object. Use catObjeForFile to retrieve the catalog entry. Then, after setting offset and alignedLine, the header must be updated. And after deleting, if the page is empty and it is not the first page of the file, you must deallocate the page.

- EduOM_NextObject
If a curOID exists, browse to the pageNo and volNo of the corresponding curOID. If not, set the first page of the catalog entry to pageNo. Then go to the page. On that page, find the object slot, not the EMPTY SLOT, from the next number of the curOID slot. If it is not on the page, browse to the next page, and return EOS if it is not on the end.

- EduOM_PrevObject
It is almost the same as NextObject. If a curOID exists, browse to the pageNo and volNo of the corresponding curOID. If not, set the first page of the catalog entry to pageNo. Then go to the page. On that page, find the object slot, not the EMPTY SLOT, from the next number of the curOID slot. If it is not on the page, browse to the prev page, and return EOS if it is not on the end.

- EduOM_ReadObject
Use the oid to read the page. And if the length is not as long as REMAINDER, read it as long as it is long, and if it is as long as REMAINDER, read it to the end and return the length.