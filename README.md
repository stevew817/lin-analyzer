# Saleae Local Interconnect Network (LIN) Analyzer

Saleae Local Interconnect Network (LIN) Analyzer

## Getting Started

### MacOS

Dependencies:
- XCode with command line tools
- CMake 3.13+

Installing command line tools after XCode is installed:
```
xcode-select --install
```

Then open XCode, open Preferences from the main menu, go to locations, and select the only option under 'Command line tools'.

Installing CMake on MacOS:

1. Download the binary distribution for MacOS, `cmake-*-Darwin-x86_64.dmg`
2. Install the usual way by dragging into applications.
3. Open a terminal and run the following:
```
/Applications/CMake.app/Contents/bin/cmake-gui --install
```
*Note: Errors may occur if older versions of CMake are installed.*

Building the analyzer:
```
mkdir build
cd build
cmake ..
cmake --build .
```

### Ubuntu 16.04

Dependencies:
- CMake 3.13+
- gcc 4.8+

Misc dependencies:

```
sudo apt-get install build-essential
```

Building the analyzer:
```
mkdir build
cd build
cmake ..
cmake --build .
```

### Windows

Dependencies:
- Visual Studio 2015 Update 3
- CMake 3.13+

**Visual Studio 2015**

*Note - newer versions of Visual Studio should be fine.*

Setup options:
- Programming Languages > Visual C++ > select all sub-components.

Note - if CMake has any problems with the MSVC compiler, it's likely a component is missing.

**CMake**

Download and install the latest CMake release here.
https://cmake.org/download/

Building the analyzer:
```
mkdir build
cd build -A x64
cmake ..
```

Then, open the newly created solution file located here: `build\lin_analyzer.sln`


## Output Frame Format
  
### Frame Type: `"no_frame"`

| Property | Type | Description |
| :--- | :--- | :--- |


Inter-byte space

### Frame Type: `"header_break"`

| Property | Type | Description |
| :--- | :--- | :--- |


Header break

### Frame Type: `"header_sync"`

| Property | Type | Description |
| :--- | :--- | :--- |


Header sync

### Frame Type: `"header_pid"`

| Property | Type | Description |
| :--- | :--- | :--- |
| `protected_id` | int | 6 bit protected Id |

Protected identifier

### Frame Type: `"data"`

| Property | Type | Description |
| :--- | :--- | :--- |
| `data` | int | Data byte |
| `index` | int | Index, 0-8, of the data byte inside of the transaction |

### Frame Type: `"checksum"`

| Property | Type | Description |
| :--- | :--- | :--- |
| `checksum` | int | LIN checksum |

Checksum byte

### Frame Type: `"data_or_checksum"`

| Property | Type | Description |
| :--- | :--- | :--- |
| `checksum` | int | LIN checksum |
| `data` | int | Data byte |
| `index` | int | Index, 0-8, of the data byte inside of the transaction |

Unable to determine if this byte is a data byte or a checksum. It is technically valid as both. This occurs if a a data byte, at index N, is equal to what the CRC should be if the transaction is N-1 bytes.

