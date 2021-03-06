# Assignment: Flat file Reader (Decrypted using hashing)
## Problem Statement
A specification for a very simple file system stored inside a flat file (FS). There is an associated index file (FI) which provides meta-data to the data inside the flat file (FS). 

FS:- FS cannot be larger than 1 MB. The entire space in FS is divided into blocks of 128 bytes. 
FI:- FI provides meta-data regarding what is stored in FS. Directories, sub-directories and files are supported. Files can be binary or text which is marked in the meta-data. The following is a detailed description of FI – 
FI consists of a sequence of entries or records. Each record (R) is 48 bytes long. Each record has an index and is referred by its index. There can be a max 8192 Records if each file is exactly one block long. Therefore FI can be at most 8192 x 48 = ~384KB in size. The structure of each R is – 

1             2  3  4    5 
|-----------------|--|--|---|-------|

1 – Name (32 bytes)
2 – Attribs (2 bytes) Described below
3 – Directory Entry (2 bytes) – what is the parent directory of this record
4 – Size (4 bytes) – File size, 0 for Directory
5 – Blocks list (8 bytes)

Name – The file/dir name can be at most 32 bytes long. Only ascii alpha-numeric characters are allowed. The only symbols allowed are - $ and . A string shorter than 32 characters is terminated with an ascii value of 0.
Attributes – Only the relevant attributes are described here
            1st bit – if set is a File else Dir
            3rd bit – if set is a Text file else Binary
Dir Entry – The index of the parent’s Record in FI. The root entry has this value as 0.
Size – The actual size of the file (not the block count), always 0 for directories
Blocks list – Lists which blocks in FS holds the contents of this record. 8 bytes allows for 4 block indices to be specified each of size 2 bytes. If a file is larger than 4 block sizes (i.e. larger than 512 bytes) then a chaining mechanism is used where the last 2 bytes of the block from FD is used to point to the next block in FS.  Suppose if the file is of 8 block size, then the last 2 bytes of 4th block will point to 5th block and last 2 bytes of 5th block points to 6th block and so on.
Directories will not have any block entries.

The root directory always occupies R[0].

Problem
A] Write a class com.test.FSReader which has a static read method and takes as its only argument a file path similar to \files\abc.txt and returns a String of its contents. If the path provided is not a file or not a text file null must be returned. No exceptions must be thrown.
Signature -> String com.test.FSReader.read(String path)

Please send the output for file path \Progress\OpenEdge\OpenEdge.txt along with Source code.

For test purposes, you can use file path \Progress\ProblemStatement.txt which returns present file contents.
