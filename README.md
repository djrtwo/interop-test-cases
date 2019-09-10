# Interop Test Cases

Collection of block type test cases from consensus errors found at interop.

In addition to the normal inputs (`pre.ssz`, `block.ssz`, `post.ssz`), each test case also contains a `notes.md` and a `bad_post.ssz`. 
`notes.ssz` discusss the conditions upon which this error was found and what is missed in the state tests.
`bad_post.ssz` documents the incorrect post state output by the client that found the error.

Each test case is in its own directory under [`/tests`](./tests).
