# Bit Mask
## Definitions:
- A mask is a bit with flag bits are 1s.
- Combine two masks using | (or)
- Substract a mask using ^ (xor)
Ex:
```java
int maskReadAllowed = 4;    // 00001000
int maskWriteAllowed = 16;  // 00010000
// 00001000 | 00010000 = 00011000 represents both read and write permissions
int maskReadAndWriteAllowed = maskReadAllowed | maskWriteAllowed;
int maskReadAllowed = maskReadAndWriteAllowed ^ maskWriteAllowed;
```
## Creating bit masks
- Mask with N ones at the end
```java
int bitMask =   ( 1 << N ) - 1;
```
- Mask with one at position N
```java
int bitMask = 1 << N ;
```
- Mask with 1 from M to N
```java
int bitMask = (( 1 << ( N - M + 1 ) ) - 1 ) << M 
```
## Operations on masks
### SET or turn on a flag bit
- Using | (OR)
```java
flags = flags | bitMask;
flags |= bitMask;
```
### UNSET or TURN OFF a flag bit
- Using & ~ ( AND INVERT )
```java
flags = flags & ~bitMask;
flags &= ~bitMask;
```
### Check the state of the flag bit
- Using & (AND)
```java
if (  (flags & bitMask) == bitMask ){

}
else {

}
```
### Toggle a flag bit
- Using | (XOR)
```java
flags ^= bitMask;
flags = flags ^ bitMask;
```
