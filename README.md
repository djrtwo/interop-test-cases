# Interop Test Cases

Collection of block type test cases from consensus errors found at interop. `post.ssz` is generated directly from the pyspec.

In addition to the normal test inputs (`pre.ssz`, `block.ssz`, `post.ssz`), each test case also contains a `README.md` and a `bad_*_post.ssz`. 
`README.ssz` discusss the conditions upon which this error was found and what is missed in the state tests.
Files of the form `bad_*_post.ssz` document the incorrect post state output by the client(s) that found the error.

Each test case is in its own directory under [`/tests`](./tests).
