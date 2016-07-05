## mitdb-get

mitdb-get is a command line tool for downloading and resampling the MIT-BIH Arrhythmia Database from [PhysioNet](https://www.physionet.org/physiobank/database/mitdb/)

### Installation

This script uses `wget` for downloading the database from [PhysioNet](https://www.physionet.org/physiobank/database/mitdb/) and  relies on the [xform utility](https://www.physionet.org/physiotools/wag/xform-1.htm) from the [WFDB software  package](http://www.physionet.org/physiotools/wfdb.shtml) to convert the downloaded files, so you will need to have those tools installed in order to use this.

### Usage

```sh
# Download all records to a "mitdb" subdir
./mitdb-get -a

# Download only some records
./mitdb-get -r 100,101,102

# Download the full db and resample it to 250Hz and 300Hz
./mitdb-get -a -f 250,300

# Use a custom download directory
./mitdb-get -r 203,207,212 -o /tmp/mitdb

```

The original files of the MIT-BIH database will be located in a 360Hz folder inside the download directory you provided (`mitdb` by default). If the `-f` option is present, a folder for each one of the provided sampling
frequencies will also be created and the converted files placed inside, as sown in the next example:

```sh
$ mitdb-get -a -o /tmp/mitdb -f 200,250,300
$ tree -a /tmp/mitdb/ -P 100*
/tmp/mitdb/
├── 200Hz
│   ├── 100.hea
│   ├── 100.dat
│   └── 100.atr
├── 250Hz
│   ├── 100.hea
│   ├── 100.dat
│   └── 100.atr
├── 300Hz
│   ├── 100.hea
│   ├── 100.dat
│   └── 100.atr
└── 360Hz
    ├── 100.hea
    ├── 100.dat
    └── 100.atr
```

As a precaution to avoid overriding existing files, resampling will be skipped if a directory with the resulting name (Ex: `250Hz`) already exists. In the same way, no files will be downloaded if a folder named `360Hz` is present in the download directory.

### Available options:

- `-a --all` Download all database records

- `-r --record recordName` Record or set of records to download (use `,` to separate more than one)

- `-f --frequency samplingFrequency` Frequency or set of frequencies to resample downloaded records (use `,` to separate more than one)

- `-o --output outputDir` Download directory

   *(One of the previous `-a` or `-r` options is required)*
