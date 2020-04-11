

SparseArray can be used to replace HashMap when the key is a primitive type. There are some variants for different key/value types, even though not all of them are publicly available.

###Benefits are:

Allocation-free
No boxing


###Drawbacks:

Generally slower, not indicated for large collections
They won't work in a non-Android project
