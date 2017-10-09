# BInt and BDouble
BInt and BDouble is a lightweight, and easy-to-use, arbitrary precision arithmetic library for Swift 3. It supports whole Numbers (BInt) and Fractions (BDouble) with most of the common math operators like addition, subtraction, multiplication, exponentiation, modulus and division. Some optimized math functions like factorial or gcd are also implemented. So more details, please continue reading.

Some benchmarks are located in Benchmarks.swift, note that these are more than 10 times faster in release mode.

### Swift Package Manager

You can use the [Swift Package Manager](https://swift.org/package-manager/) and specify the  package dependency in your `Package.swift` file by adding this:
```swift
.Package(url: "https://github.com/schwenger/Swift-Big-Integer.git", from: "1.0.0")
```


## Usage
This subsection explains the usage of BInt and BDouble

### BInt

#### You can initialize BInt with the following constructors:
```swift
BInt(Int)
BInt(UInt)
BInt(String)
```

#### Examples:
```swift
let i = BInt(12)
let i = BInt(-9234)
let i = BInt("-2343241765837645983267582365876326491813491053680428560284652986203287826526")
```

#### BInt offers 7 struct methods:
```swift
let big = BInt("-143141341")

big.description // Returns "-143141341"
=> print(big) // prints "-143141341"

big.toInt() // returns -143141341 (only works when Int.min <= big <= Int.max)

big.isPositive() // Returns false
big.isNegative() // Returns true
big.isZero() // Returns false

big.negate() // Returns noting, but negates the BInt (mutating func)

big.rawData() // Returns internal structure
```

### The following Operators work with BInt:
```swift
// Operating on Int and BInt result in a typecast to BInt

// Addition
BIntOrInt  +  BIntOrInt // Returns BInt
BIntOrInt  += BIntOrInt

//Subtraction
BIntOrInt  -  BIntOrInt // Returns BInt
BIntOrInt  -= BIntOrInt

// Multiplication
BIntOrInt  *  BIntOrInt // Returns BInt
BIntOrInt  *= BIntOrInt

// Powering
BInt       ^  Int       // Returns BInt to the power of Int

// Modulo
BIntOrInt  %  BIntOrInt // Returns BInt
BInt       %= BInt

// Division
BInt       /  BInt // Returns BInt
BInt       /= BInt


// Comparing
BInt       == BInt
BInt       != BInt
BInt       <  BInt
BInt       <= BInt
BInt       >  BInt
BInt       >= BInt
```

#### Implemented BInt math functions:
```swift
fact(Int) // Returns factorial as BInt

gcd(BInt, BInt) // Returns greatest common divisor as BInt

lcm(BInt, BInt) // Returns lowest common multiple as BInt

permutations(BInt, BInt) // Returns BInt

combinations(BInt, BInt) // Returns BInt
```

#### Compatibility with Bignum

`BInt` has a typealias to `Bignum` that is largely drop-in compatible with the OpenSSL-based [Swift big number library](https://github.com/Bouke/Bignum).  The following properties and operations are available on `BInt`/`Bignum`:

```swift
public var data: Data				/// Representation as big-endian Data
public var dec: String				/// Decimal string representation
public var hex: String				/// Hexadecimal string representation

public init(hex: String)			/// Initialise a new BInt from a hexadecimal string
public init(_ n: UInt64)			/// Initialise from an unsigned, 64 bit integer
public init(data: Data)				/// Initialise from big-endian Data

/// Combined exponentiation/modulo algorithm
///
/// - Parameters:
///   - b: base
///   - p: power
///   - m: modulus
/// - Returns: pow(b, p) % m
public func mod_exp(_ b: BInt, _ p: BInt, _ m: BInt) -> BInt

/// Non-negative modulo operation
///
/// - Parameters:
///   - a: left hand side of the module operation
///   - m: modulus
/// - Returns: r := a % b such that 0 <= r < abs(m)
public func nnmod(_ a: BInt, _ m: BInt) -> BInt
```

### BDouble

#### BDouble allows these constructors:
```swift
BDouble(Int)
BDouble(Double)
BDouble(Int, over: Int)
BDouble(String, over: String)
```

#### Examples:
```swift
let d = BDouble(221)
let d = BDouble(1.192)
let d = BDouble(3, over: 4)
let d = BDouble("1" over: "3421342675925672365438867862653658268376582356831563158967")
```

#### BDouble offers these struct methods:
```swift
let bigD = BDouble(-12.32)

bigD.description // Returns "-308/25"
=> print(bigD) // prints "-308/25"


bigD.minimize() // Divides numerator and denominator by their gcd for storage and operation efficiency, usually not necessary, because of automatic minimization

big.rawData() // Returns internal structure
```

### The following Operators work with BDouble:
```swift
// Needs more operators, interoperability with BInt

// Addition
BDouble + BDouble // Returns BDouble

// Subtraction
BDouble - BDouble // Returns BDouble

// Multiplication
BDouble * BDouble // Returns BDouble

// Division
BDouble / BDouble // Returns BDouble

// Comparing
BDouble < BDouble
/*
Important:
a < b <==> b > a
a <= b <==> b >= a
but:
a < b <==> !(a >= b)
a <= b <==> !(a > b)
*/

// More will follow
```



## About performance
BInt about twice as fast as mini-gmp, as of now (not counting the normal GMP, because it needs to be installed and is not portable). For example, BInt can add numbers about 2 times faster than GMP (272ms vs 530ms for fib(100,000)), and multiply more than 2 times faster. When given the task of calculating and printing factorials successively, BInt performs significantly better than GMP. In addition, GMP is significantly harder to use, especially in combination with Swift, while BInt offers an intuitive interface.


# About this fork
This project was forked in order to comply to our needs. No further feature development is to be expected.
