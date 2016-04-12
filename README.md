# Npr2Pcode-machine
An simple approach to translate reverse polish notation in pcode instructions

# Assumptions
* Pcode machine has a correct reverse polish notation as input
* ~ is an unary operator (Neg), that is, need at least one number on stack to proceed
* + - * / are binary operators, that is, need at least two numbers on stack to proceed
* The rightmost integer on stack will be load first (See division example)

# Compiling
gcc -o npr2pcode npr2pcode.c

# Running
./npr2pcode

# Examples
```
Notation: 5 ~

Output:
Inst       Level           Arg             Top             Counter         Stack
INT        0               3               0               1               0 0 0 
LIT        0               5               5               2               0 0 0 5 
STO        0               0               0               3               5 0 0 
LOD        0               0               5               4               5 0 0 5 
OPR        0               1               -5              5               5 0 0 -5 
STO        0               0               0               6               -5 0 0

```
```
Notation: 20 4 /

Output: 
Inst       Level           Arg             Top             Counter         Stack
INT        0               6               0               1               0 0 0 0 0 0 
LIT        0               20              20              2               0 0 0 0 0 0 20 
STO        0               0               0               3               20 0 0 0 0 0 
LIT        0               4               4               4               20 0 0 0 0 0 4 
STO        0               1               0               5               20 4 0 0 0 0 
LOD        0               1               4               6               20 4 0 0 0 0 4 
LOD        0               0               20              7               20 4 0 0 0 0 4 20 
OPR        0               5               0               8               20 4 0 0 0 0 0 
STO        0               2               0               9               20 4 0 0 0 0

```
```
Notation: 4 20 /

INT        0               6               0               1               0 0 0 0 0 0 
LIT        0               4               4               2               0 0 0 0 0 0 4 
STO        0               0               0               3               4 0 0 0 0 0 
LIT        0               20              20              4               4 0 0 0 0 0 20 
STO        0               1               0               5               4 20 0 0 0 0 
LOD        0               1               20              6               4 20 0 0 0 0 20 
LOD        0               0               4               7               4 20 0 0 0 0 20 4 
OPR        0               5               5               8               4 20 0 0 0 0 5 
STO        0               2               0               9               4 20 5 0 0 0 

```
```
Notation: 10 10 + ~ 5 *

Output: 
Starting the P-code Machine.
Inst       Level           Arg             Top             Counter         Stack
INT        0               13              0               1               0 0 0 0 0 0 0 0 0 0 0 0 0 
LIT        0               10              10              2               0 0 0 0 0 0 0 0 0 0 0 0 0 10 
STO        0               0               0               3               10 0 0 0 0 0 0 0 0 0 0 0 0 
LIT        0               10              10              4               10 0 0 0 0 0 0 0 0 0 0 0 0 10 
STO        0               1               0               5               10 10 0 0 0 0 0 0 0 0 0 0 0 
LOD        0               1               10              6               10 10 0 0 0 0 0 0 0 0 0 0 0 10 
LOD        0               0               10              7               10 10 0 0 0 0 0 0 0 0 0 0 0 10 10 
OPR        0               2               20              8               10 10 0 0 0 0 0 0 0 0 0 0 0 20 
STO        0               2               0               9               10 10 20 0 0 0 0 0 0 0 0 0 0 
LOD        0               2               20              10              10 10 20 0 0 0 0 0 0 0 0 0 0 20 
OPR        0               1               -20             11              10 10 20 0 0 0 0 0 0 0 0 0 0 -20 
STO        0               2               0               12              10 10 -20 0 0 0 0 0 0 0 0 0 0 
LIT        0               5               5               13              10 10 -20 0 0 0 0 0 0 0 0 0 0 5 
STO        0               3               0               14              10 10 -20 5 0 0 0 0 0 0 0 0 0 
LOD        0               3               5               15              10 10 -20 5 0 0 0 0 0 0 0 0 0 5 
LOD        0               2               -20             16              10 10 -20 5 0 0 0 0 0 0 0 0 0 5 -20 
OPR        0               4               -100            17              10 10 -20 5 0 0 0 0 0 0 0 0 0 -100 
STO        0               4               0               18              10 10 -20 5 -100 0 0 0 0 0 0 0 0 
```

