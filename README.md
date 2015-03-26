# codem-isoboxer

* http://github.com/madebyhiro/codem-isoboxer

## Description

Codem-isoboxer is a small browser-based MPEG-4 (ISOBMFF) parser. It is meant to be small, fast and efficient. A typical use-case would be inclusion in a new player framework (for emerging standards such as MPEG-DASH which rely on ISOBMFF for most situations) or to extract metadata from MPEG-4 files.

Currently a limited set of ISOBMFF boxes is supported (alphabetically):

### ISO/IEC 14496-12:2012 (ISOBMFF)
* free / skip
* ftyp / styp
* mdat
* mdia
* mdhd
* moov / moof
* mvhd / mfhd
* sidx
* tfhd / tkhd
* tfdt
* traf / trak
* trun

### ISO/IEC 23009-1:2014 (MPEG-DASH)

* emsg

Support for more boxes can easily be added by adding additional box parsers in `src/iso_box.js`. Several utility functions are included to help with reading the various ISOBMFF data types from the raw file.

## Requirements

A modern web browser with support for:

* ArrayBuffer
* DataView

## Usage

Include one of the files in the `dist` folder (regular or uglified) in your web page/application:

    <script type="text/javascript" src="iso_boxer.min.js"></script>

Then, you can parse a file by calling the `create` function:

    var parsedFile = ISOBoxer.create(arrayBuffer);

The `arrayBuffer` can for example be obtained by issuing an XHR request, or by using the `FileReader` API to read a local file.

Codem-isoboxer makes no assumptions on the validity of the given file and/or segment. It also does minimal handling of the data
types and provides mostly a raw interface. Some frequently used attributes are parsed to easier-to-use types, such as the major
brand and list of compatible brands in the `ftyp` box.

## Development

Check out the source from Github. Make changes to the files in `/src`. We use `grunt` to build the distribution files. If you add a box parser be sure to include a comment that points toward the relevant section in the specs. And if at all possible add a (small!) file to `test/fixtures` to provide an example.

### Building

    grunt

### Using grunt watcher

You can use `grunt-contrib-watch` to watch for changes to the source and automatically build it:

    grunt watch

## Demo

Open `test/index.html` in your browser. Use the file picker to select a local MPEG-4 file to parse it. Results will be in the `window.parsedFile` variable. Inspect it from your browser's console. Some test files are included in `test/fixtures`.

## License

Codem-isoboxer is released under the MIT license, see `LICENSE.txt`.
