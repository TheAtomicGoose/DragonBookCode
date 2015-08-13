Chapter 1
========

###*1.1*
`position = initial + rate * 60`

This is just an example statement with hypothetical variables.

###*1.2*
`<id, 1> <=> <id, 2> <+> <id, 3> <*> <60>`

The lexemes that the lexical analyzer would break statement `1.1` into. 

Variable | Assignment
---------|-----------
position | id1
initial  | id2
rate     | id2

###*1.3*
```
t1 = inttofloat(60)
t2 = id3 * t1
t3 = id2 + t2
id1 = t3
```

The *three-address instructions* that the statement in `1.1` would be broken into during intermediate code generation.

###*1.4*
```
t1 = id3 * 60.0
id1 = id2 + t1
```

One possible optimized version of the code in `1.3`.

###*1.5*
```
LDF  R2,  id3
MULF R2,  R2, #60.0
LDF  R1,  R1, id2
ADDF R1,  R1, R2
STF  id1, R1
```

 Command |      Meaning      
---------|-------------------
LD       | Load into register
MUL      | Multiply          
ADD      | Add				 
ST       | Store 


The `F` at the end of each command means that we're dealing with floats. The `R` stands for register, and the first argument (first thing after the command) is the place where the result of the operation is being stored.

###*1.9*
```C
...
int i;				/* global i		   */
...
void f(...) {
	int i;          /* local i         */ 
	...
	i = 3;          /* use of local i  */
	...
}
...
x = i + 1;          /* use of global i */ 
```

In this example, the variable `i` has two different scopes based upon where it is used. The global version, which is defined outside of the function `f(...) {...}`, will be referenced whenever `i` is used outside of that function. However, since `i` is defined separately inside of `f(...) {...}`, when `i` is used inside of that function, it will refer to the version of `i` defined inside the function.