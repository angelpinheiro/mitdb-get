## mitdb-get

mitdb-get is a coomand line tool for downloading and resampling the MIT-BIH Arrhythmia Database from [PhysioNet](https://www.physionet.org/physiobank/database/mitdb/)

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


### Available options:

- `-a --all` Download all database records

- `-r --record recordName` Record or set of records to download (use `,` to separate more than one)

- `-f --frequency samplingFrequency` Frequency or set of frequencies to resample downloaded records (use `,` to separate more than one)

- `-o --output outputDir` Download directory

   *(One of the previous `-a` or `-r` options is required)*
