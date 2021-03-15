# `kpipe`

This `kpipe` module combines the current versions of the main core modules of the kpipe data processing system. Including this module in a project will enable the project to use the base kpipe functionality without managing dependencies of the individual modules.

The modules included are:

| Module | Description |
|---|---
| `kpipe-core` | Storage backends and basic readable and writable stream implementations. |
| `kpipe-streams` | A set of low-level node transform streams to perform basic data conversion tasks such as compression, JSON translation, delineation, etc. |
| `kpipe-sequence` | Provides an enhanced node pipeline running as a promise as well as tools to sequence a list of promisified actions. |
| `kpipe-url` | Defines and supports a URL syntax for the kpipe stream backends. It automatically pipes together appropriate streams to deliver data in a particular format to/from a kpipe storage backend. |

---------------
## `kpipe-core`

Support for reading and writing to storage backends using standard node streams. 

Supported backends:

| Backend | Description |
|---|---|
| `stdio` | |
| `fs` | |
| `s3` | |
| `kafka` | |
| `buffer` | |
| `random` | |

| Function | Description |
|---|---|
| `Reader` | |
| `Writer` | |
| `KafkaProducer` | |
| `KafkaAdmin` | |

-------------
## `kpipe-streams`

Supported transforms:

| Transform | Description |
|---|---|
| `Lineate` | Add newlines to incoming strings and pack into a buffer |
| `Delineate` | Split buffer into individual strings delimited by newlines |
| `JSONParse` | Parse an incoming JSON string into a JavaScript object |
| `JSONStringify` | Generate a JSON string from incoming JavaScripts objects |
| `Gzip` | Compress a buffer stream using the zlib library |
| `Gunzip` | Decompress a buffer stream using the zlib library |
| `SnappyCompress` | Compress a buffer with snappy |
| `SnappyDecompress` | Decompress a buffer with snappy |

-----------------------------
## `kpipe-sequence`

### `PipelinePromise`

### `PromiseChain`

------------------------------
## `kpipe-url`

Translate URL-like paths into Kpipe backend stream generators.

| Pattern | Backend | Description |
|---|---|---|
| stdio://  <br/> - | `stdio` | |
| fs://[path]/[file].[ext] <br/> file://[path]/[file].[ext] | `fs` | |
| s3://[bucket]\(/[prefix]\)/[file].[ext] | `s3` | |
| kafka://[topic]\(/[partition]\(/[offset]\)\)| `kafka` | |

| Function | Description |
|---|---|
| `readerUrl` | Return a Reader stream generator given a kpipe url |
| `readStreamUrl` | Return a readable stream given a kpipe url |
| `writerUrl` | Return a Writer stream generator given a kpipe url |
| `writeStreamUrl` | Return a writable stream given a kpipe url |
| `urlInStreams` | Given a kpipe url, return a readable stream which transforms backend data into the supplied content format (`buffer`, `strings`, or `json`) |
| `urlOutStreams` | Given a kpipe url, return a writable stream which transforms data from the supplied content format (`buffer`, `strings`, or `json`) to a kpipe backend |
| `urlOutMultiplex` | Special case of `urlOutStreams` which splits the incoming stream into one or more destination streams |
| `urlPipeline` | Given an input URL, some transforms, and an output URL, return a promisified pipeline which performs a data conversion task |
| `urlPipelineSorted` | Given an input URL, some transforms, and an output URL, return a promisified pipeline which first sorts the entire incoming dataset and then performs a data conversion task |
| `parseUrl` | Helper function returns the parsed components of a kpipe url |
| `contentModifiers` | Helper function returns an array of transforms to convert streams from one of the three content types (`buffer`, `strings`, or `json`) into another content type. |
| `compressExt` | Helper function returns a transform stream (or passthrough) which compresses content according to a supplied filename extension |
| `decompressExt` | Helper function returns a transform stream (or passthrough) which decompresses content according to a supplied filename extension |




