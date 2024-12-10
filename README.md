# DV2str - A DV Timecode Extractor Tool

## Table of Content
- [Why do I Need this Tool?](#why-do-i-need-the-dv-timecode-extractor-tool)
- [Features](#features)
- [How DV2str Works](#how-dv2str-works)
- [(.avi) file format - Header References](#avi-file-format---header-references)
- [DV Format in .avi](#dv-format-in-avi)
- [Main Functions](#main-functions)
- [Code Structure](#code-structure)
- [How to Install](#how-to-install)
- [Output Examples](#output-examples)
- [License](#license)
- [Authors & Contributors](#authors--contributors)


## Why do I need the DV Timecode Extractor Tool?

The **DV Timecode Extractor Tool** is a program developed in **Python**, and later on converted to **C++**, to extract the **timecode** data (following the **DD** / **MM** / **YYYY** **HH** : **mm** : **ss** Format) from **DV video streams**, encapsulated in **.avi** files, and generate **.srt** files, that could be ser embedded in **.mp4** containers.

## Features

- Precise extraction of Date timecodes, directly from DV (**.avi**) into **.srt** files.
- Offers support for both **NTSC** and **PAL** streaming systems.


---


## How DV2str Works

1. The **.avi** file is opened
2. The header is analysed, cycling through the most relevant **chunks**.
3. It searches for subcode packages (such as **pack62** and **pack63**), which hold all the **Time and Date** information from the file.
4. It **decodes and checks for any errors** in the extracted data, **returning the timecode** formated on a more readable state.
5. The Information is then ready to be **exported as a .srt file**, or used in any other way intended.


## (.avi) file format - Header References

NOTE: All the following references are based on **.avi** File Format Research Databases.
Go on (https://xoax.net/sub_web/ref_dev/fileformat_avi/) to find more information regarding the Audio Video Interleave (avi) File Format.
- **RIFF Header**: Defines the file as an **.avi** type
- **Chunks "hdrl"**: Contains all metadata from the file (such as the it's resolution, etc...)
- **Chunks "movi"**: Contains all Multiplexed Audio and Video data.
- **Chunks "idx1"**: Although optional, it can be used to index the frames, making navigation on the file much more efficient.


## DV Format in .avi
The DV format encapsulates digital video (DV) in data packets with a specific structure. Each DV frame contains timecode subcodes that can be extracted for use in editing or analysis.

The DV Data Extraction Process:
- Identify video data chunks in the **.avi** file (typically located in the "movi" chunk).
- Read 80-byte DV packets, which include:
  - Timecodes: Information such as hour, minute, second, and frame number.
  - Auxiliary subcodes: Used for synchronization and error correction.

NOTE: The source code in this project uses logic similar to that found in WinDV(https://github.com/hfiggs/WinDV/blob/main/DV.cpp) to identify and interpret encapsulated DV packets.


### Main Functions
- **get_dv_recording_time(data, name, offset)**: Extracts and verifies the Date and Time from the data stream.
- **get_ssyb_pack(data, pack_num)**: Finds specific subcode packages on the stream.
- **parse_riff_header(file)**: Analyses the RIFF Header from the file.
- **parse_idx1(file, offset)**: Locates the chunks index on the file.


---


## Code Structure
- **Reads & Decodes** the **.avi** file.
- **Extacts** the **timecode**.
- **Analyses** all data to ensure consistency, and to **avoid any faults**.


---


## How to Install

1. **First, make sure you have:**
    - Python 3.x installed.
    - NOTE: It is not mandatory (but certainly advisable) that all the main Python Libraries are already pre-installed and fully working on your device.

2. **Clone this repository using git (NOTE: although not recommended, you can opt to download this repository directly from the GitHub source).**

3. **Execute the main script**:
    ```bash
    python main.py <path_to_the_avi_file>
    ```

4. **Output**:
   - The Date and timecode will then be shown on your device's Terminal.


---


## Output Examples

If/While processing an uncorrupted DV/.avi file, this is an example of what to expect from an Output Stream:

**Processing video chunk video1 at offset 1000, size 144000 bytes Timecode: 12/05/2007 14:32:45**


---


# License
MIT License

Copyright (c) 2024 DV2str

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---


# Authors & Contributors
- José Rodrigues (Msc in Computer Science, @University of Coimbra) - Author
- Tomás Gonçalves (Bsc in Computer Science, @University of Coimbra) - Contributor
