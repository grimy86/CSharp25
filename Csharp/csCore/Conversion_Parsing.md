# Type conversion and parsing
```cs
//Implicit
int num = 2147483647;
long bigNum = num;

//Explicit
double x = 1234.7;
a = (int)x;

//Derivative
Giraffe g = new Giraffe();
Animal a = g; // class Giragge : Animal <- base

//TryParse vs. Parse methods
//If the type cannot be converted, then the type.TryParse method returns false whereas the parse method will return an exception.
int res;
string myStr = "120";
res = int.Parse(myStr); //Returns an exception if the parse fails.
```
| Type conversion methods |
|-----------|
| ToBoolean |
| ToByte    |
| ToChar    |
| ToDateTime|
| ToDecimal |
| ToDouble  |
| ToInt16   |
| ToInt32   |
| ToInt64   |
| ToSbyte   |
| ToSingle  |
| ToString  |
| ToType    |
| ToUInt16  |
| ToUInt32  |
| ToUInt64  |