# rocksdb

rocksdb is a Go wrapper for rocksdb.

This is a fork of [InfluxDB's port](http://godoc.org/github.com/influxdb/rocksdb) which is in turn a fork/modification of [levigo](http://github.com/jmhodges/levigo)

The API has been godoc'ed and [is available on the
web](http://godoc.org/github.com/pandemicsyn/rocksdb).


## Building

You'll need the shared library build of
[RocksDB](http://github.com/facebook/rocksdb/) installed on your machine.


Now, if you build LevelDB and put the shared library and headers in one of the
standard places for your OS, you'll be able to simply run:

    go get github.com/pandemicsyn/rocksdb

But, suppose you put the shared LevelDB library somewhere weird like
/path/to/rocksdb and the headers were installed in /path/to/rocksdb/include. To install
rocksdb remotely, you'll run:

    CGO_CFLAGS="-I/path/to/rocksdb/include" CGO_LDFLAGS="-L/path/to/rocksdb/lib" go get github.com/pandemicsyn/rocksdb

and there you go.

Of course, these same rules apply when doing `go build`, as well.

## Caveats

Comparators and WriteBatch iterators must be written in C in your own
library. This seems like a pain in the ass, but remember that you'll have the
LevelDB C API available to your in your client package when you import levigo.

An example of writing your own Comparator can be found in
<https://github.com/jmhodges/levigo/blob/master/examples>.
