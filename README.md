# fasthash
Go package porting the standard hashing algorithms to a more efficient implementation.

## Motivations

Go has great support for hashing algorithms in the standard library, but the
APIs are all exposed as interfaces, which means passing strings or byte slices
to those require dynamic memory allocations. Hashing a string typically requires
2 allocations, one for the Hash value, and one to covert the string to a byte
slice.

This package attempts to solve this issue by exposing functions that implement
string hashing algorithms and don't require dynamic memory alloations.

## Testing

To ensure consistency between the `fasthash` package and the standard library,
all tests must be implemented to run against the standard hash functions and
validate that both packages produced the same results.

## Benchmarks

The implementations also have to prove that they are more efficient in terms of
CPU and memory usage than the functions found in the standard library.  
Here's an example with fnv-1a:
```
BenchmarkHash64/standard_hash_function 20000000   105.0 ns/op   342.31 MB/s   56 B/op   2 allocs/op
BenchmarkHash64/hash_function          50000000    38.6 ns/op   932.35 MB/s    0 B/op   0 allocs/op
```
