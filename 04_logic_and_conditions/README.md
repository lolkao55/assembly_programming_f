# 04_logic_and_conditions examples

|Operation|Flag Raised|Result produced|Reason|
|:---|:---:|:---:|---:|
|AND|PF,SF|10001000|Had even no. of ones and the MSB=1|
|NOT|None|01010101|It does not modify the status flags|
|OR|PF,SF|11101110|Even no. of flags and MSB=1|
|TEST|PF|**No result stored**|Performs bitwise AND.Have two '1's' which are even|
|XOR|PF|01100110|Two values must be different bitwise.Have four '1's' which are even|