# NASDAQ TotalView-ITCH 5.0 parsers written in Go

Here is a parser of NASDAQ TotalView-ITCH 5.0 outbound data feeds, written
in Go. The specification for NASDAQ TotalView-ITCH 5.0 can
be found at <https://www.nasdaqtrader.com/content/technicalsupport/specifications/dataproducts/NQTVITCHspecification.pdf>.

All integer fields in ITCH data feeds are big-endian (network byte order)
binary encoded numbers. Unless otherwise noted, they are unsigned.

## Notes on the Implementation

In the Go implementation, we use the [encoding/binary](https://golang.org/pkg/encoding/binary/)
package of the [Go Standard Library](https://golang.org/pkg/#stdlib) to
convert big-endian integers to little-endian.

You can build the Go parser with:

```console
go build parseITCH5.go
```

## Usage

Running the executable without any argument will show you the usage:

```console
$ ./parse_itch5
Usage: ./parse_itch5 input_file_path output_folder_path [msg_types]

If msg_types is not provided, output will be generated for all types
```

For example, to parse all messages in the daily feed *S051018-v50.txt*, and
saved the parsed CSV files in folder *output*:

```console
./parse_itch5 /path/to/S051018-v50.txt output
```

If you only want to parse messages of type `R` and `A`:

```console
./parse_itch5 /path/to/S051018-v50.txt output RA
```
