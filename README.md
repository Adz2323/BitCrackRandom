# BitCrackRandom using New Generation Graphics CARD
I ALSO HAVE ZEROOO idea of what im doing but i wanted a BitCrack with a random feature so i saw this Fork but didnt work so i made changes until it worked (i use LINUX Ubuntu)

Puzzle #66
after you have made the file run

./bin/cuBitCrack -c 13zb1hQbWVsc2S7ZTZnP2G4undNNpdh5so --keyspace 20000000000000000:3FFFFFFFFFFFFFFFF -r 



:~/BitCrack/new/BitCrack# ./bin/cuBitCrack -c 13zb1hQbWVsc2S7ZTZnP2G4undNNpdh5so --keyspace 30000000000000000:3FFFFFFFFFFFFFFFF -r
[2023-11-10.18:41:41] [Info] Compression: compressed
[2023-11-10.18:41:41] [Info] Starting at: 0000000000000000000000000000000000000000000000030000000000000000
[2023-11-10.18:41:41] [Info] Ending at:   000000000000000000000000000000000000000000000003FFFFFFFFFFFFFFFF
[2023-11-10.18:41:41] [Info] Counting by: 0000000000000000000000000000000000000000000000000000000000000001
[2023-11-10.18:41:41] [Info] Generating random starting points
[2023-11-10.18:41:41] [Info] Initializing NVIDIA GeForce RTX 4090
[2023-11-10.18:41:41] [Info] Generating 134,217,728 starting points (5120.0MB)
[2023-11-10.18:41:41] [Info] Starting point sample: 000000000000000000000000000000000000000000000003D909120FE6B4D0FA (66 bit range)
[2023-11-10.18:41:41] [Info] Starting point sample: 00000000000000000000000000000000000000000000000391534306231962A3 (66 bit range)
[2023-11-10.18:41:41] [Info] Starting point sample: 00000000000000000000000000000000000000000000000340C24672AC4CCBF0 (66 bit range)
[2023-11-10.18:42:21] [Info] 10.0%
[2023-11-10.18:42:23] [Info] 20.0%
[2023-11-10.18:42:23] [Info] 30.0%
[2023-11-10.18:42:24] [Info] 40.0%
[2023-11-10.18:42:24] [Info] 50.0%
[2023-11-10.18:42:24] [Info] 60.0%
[2023-11-10.18:42:24] [Info] 70.0%
[2023-11-10.18:42:25] [Info] 80.0%
[2023-11-10.18:42:25] [Info] 90.0%
[2023-11-10.18:42:25] [Info] 100.0%
[2023-11-10.18:42:25] [Info] Done
NVIDIA GeForce R 12677 / 24217MB | 1 target 3526.25 MKey/s (61,209,592,201,216 total) [04:49:10]

Puzzle #66


# Previous fork
I have absolutely no idea what I'm doing. The edits to this repo are for CUDA only. Borrowing from various other tweaks found in the mass of forks for BitCrack. No clue if they'll even work or not. . . Let's find out! - DL

Contains tweaks from the following forks: ByLamacq, Radrigo, frstrtr (not implemented in .exe; you'll have to rename main_alt to main and compile), L0laapk3, and any others that have made apparent improvements to the original by brichard19. All of you are wizards and I bow to your superior abilities!

This code also incorporates the popular but now removed pikachunakapika fork containing random mode along with the other tweaks. I found the source in the closed pull request in the original brichard19 repo. https://github.com/brichard19/BitCrack/pull/148/files

# BitCrack

A tool for brute-forcing Bitcoin private keys. The main purpose of this project is to contribute to the effort of solving the [Bitcoin puzzle transaction](https://blockchain.info/tx/08389f34c98c606322740c0be6a7125d9860bb8d5cb182c02f98461e5fa6cd15): A transaction with 32 addresses that become increasingly difficult to crack.


### Using BitCrack

#### Usage


Use `cuBitCrack.exe` for CUDA devices and `clBitCrack.exe` for OpenCL devices.

### Note: **clBitCrack.exe is still EXPERIMENTAL**, as users have reported critial bugs when running on some AMD and Intel devices.

**Note for Intel users:**

There is bug in Intel's OpenCL implementation which affects BitCrack. Details here: https://github.com/brichard19/BitCrack/issues/123


```
xxBitCrack.exe [OPTIONS] [TARGETS]

Where [TARGETS] are one or more Bitcoin address

Options:

-i, --in FILE
    Read addresses from FILE, one address per line. If FILE is "-" then stdin is read

-o, --out FILE
    Append private keys to FILE, one per line

-d, --device N
    Use device with ID equal to N

-b, --blocks BLOCKS
    The number of CUDA blocks

-t, --threads THREADS
    Threads per block

-p, --points NUMBER
    Each thread will process NUMBER keys at a time
    
-r, --random
    Each point will start in random KEYSPACE

--keyspace KEYSPACE
    Specify the range of keys to search, where KEYSPACE is in the format,

	START:END start at key START, end at key END
	START:+COUNT start at key START and end at key START + COUNT
    :END start at key 1 and end at key END
	:+COUNT start at key 1 and end at key 1 + COUNT

-c, --compressed
    Search for compressed keys (default). Can be used with -u to also search uncompressed keys

-u, --uncompressed
    Search for uncompressed keys, can be used with -c to search compressed keys

--compression MODE
    Specify the compression mode, where MODE is 'compressed' or 'uncompressed' or 'both'

--list-devices
    List available devices

--stride NUMBER
    Increment by NUMBER

--share M/N
    Divide the keyspace into N equal sized shares, process the Mth share

--continue FILE
    Save/load progress from FILE
```

#### Examples

The simplest usage, the keyspace will begin at 0, and the CUDA parameters will be chosen automatically
```
xxBitCrack.exe 1FshYsUh3mqgsG29XpZ23eLjWV8Ur3VwH
```

Multiple keys can be searched at once with minimal impact to performance. Provide the keys on the command line, or in a file with one address per line
```
xxBitCrack.exe 1FshYsUh3mqgsG29XpZ23eLjWV8Ur3VwH 15JhYXn6Mx3oF4Y7PcTAv2wVVAuCFFQNiP 19EEC52krRUK1RkUAEZmQdjTyHT7Gp1TYT
```

To start the search at a specific private key, use the `--keyspace` option:

```
xxBitCrack.exe --keyspace 766519C977831678F0000000000 1FshYsUh3mqgsG29XpZ23eLjWV8Ur3VwH
```

The `--keyspace` option can also be used to search a specific range:

```
xxBitCrack.exe --keyspace 80000000:ffffffff 1FshYsUh3mqgsG29XpZ23eLjWV8Ur3VwH
```

To periodically save progress, the `--continue` option can be used. This is useful for recovering
after an unexpected interruption:

```
xxBitCrack.exe --keyspace 80000000:ffffffff 1FshYsUh3mqgsG29XpZ23eLjWV8Ur3VwH
...
GeForce GT 640   224/1024MB | 1 target 10.33 MKey/s (1,244,659,712 total) [00:01:58]
^C
xxBitCrack.exe --keyspace 80000000:ffffffff 1FshYsUh3mqgsG29XpZ23eLjWV8Ur3VwH
...
GeForce GT 640   224/1024MB | 1 target 10.33 MKey/s (1,357,905,920 total) [00:02:12]
```


Use the `-b,` `-t` and `-p` options to specify the number of blocks, threads per block, and keys per thread.
```
xxBitCrack.exe -b 32 -t 256 -p 16 1FshYsUh3mqgsG29XpZ23eLjWV8Ur3VwH
```

### Choosing the right parameters for your device

GPUs have many cores. Work for the cores is divided into blocks. Each block contains threads.

There are 3 parameters that affect performance: blocks, threads per block, and keys per thread.


`blocks:` Should be a multiple of the number of compute units on the device. The default is 32.

`threads:` The number of threads in a block. This must be a multiple of 32. The default is 256.

`Keys per thread:` The number of keys each thread will process. The performance (keys per second)
increases asymptotically with this value. The default is 256. Increasing this value will cause the
kernel to run longer, but more keys will be processed.


### Build dependencies

Visual Studio 2019 (if on Windows)

For CUDA: CUDA Toolkit 10.1

For OpenCL: An OpenCL SDK (The CUDA toolkit contains an OpenCL SDK).


### Building in Windows

Open the Visual Studio solution.

Build the `clKeyFinder` project for an OpenCL build.

Build the `cuKeyFinder` project for a CUDA build.

Note: By default the NVIDIA OpenCL headers are used. You can set the header and library path for
OpenCL in the `BitCrack.props` property sheet.

Add'l note for djarumlights fork: I could not get it to build using the project. Had to build the whole solution. 

### Building in Linux

Using `make`:

Build CUDA:
```
make BUILD_CUDA=1
```

Build OpenCL:
```
make BUILD_OPENCL=1
```

Or build both:
```
make BUILD_CUDA=1 BUILD_OPENCL=1
```

### Supporting this project

If you find this project useful and would like to support it, consider making a donation. Your support is greatly appreciated!

**BTC**: `1LqJ9cHPKxPXDRia4tteTJdLXnisnfHsof`

**LTC**: `LfwqkJY7YDYQWqgR26cg2T1F38YyojD67J`

**ETH**: `0xd28082CD48E1B279425346E8f6C651C45A9023c5`

### Contact

Send any questions or comments to bitcrack.project@gmail.com
