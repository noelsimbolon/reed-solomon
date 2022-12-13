# Reed-Solomon Code

This is a simple and efficient Reed-Solomon implementation in Java,
which was originally built at [Backblaze](https://www.backblaze.com).

The `ReedSolomon` class does the encoding and decoding, and is supported
by `Matrix`, which does matrix arithmetic, and `Galois`, which is a finite
field over 8-bit values.

For examples of how to use `ReedSolomon`, take a look at `SampleEncoder`
and `SampleDecoder`.  They show, in a very simple way, how to break a
file into shards and encode parity, and then how to take a subset of
the shards and reconstruct the original file.

There is a Gradle build file to make a jar and run the tests.  Running
it is simple.  Just type: `gradle build`

If you'd like an intro into how it all works, take a look at
[this introductory paper](http://web.eecs.utk.edu/~plank/plank/papers/SPE-9-97.html).

This project is limited to a pure Java implementation.  If you need
more speed, and can handle some assembly-language programming,
you may be interested in using the Intel SIMD instructions to speed
up the Galois field multiplication.  You can read more about that 
in the paper on [Screaming Fast Galois Field Arithmetic](http://www.kaymgee.com/Kevin_Greenan/Publications_files/plank-fast2013.pdf).

## Performance Notes

The performance of the inner loop depends on the specific processor
you're running on.  There are twelve different permutations of the
loop in this library, and the `ReedSolomonBenchmark` class will tell
you which one is faster for your particular application.  The number
of parity and data shards in the benchmark, as well as the buffer
sizes, match the usage at Backblaze.  You can set the parameters of
the benchmark to match your specific use before choosing a loop
implementation. 
