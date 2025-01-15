# Hardware
ESP32 WROVER or WROOM serie 
SPI Flash Winbond W25Q128
USB-to-UART chip (?)
Very small screen
Controller (need at least 4 directional arrows)

# File specs

## Algorithms

AES-KDF
ChaCha20

## Header

Fixed size

| Ox76617562 | File signature                    | u32       | Clear     |
| ---------- | --------------------------------- | --------- | --------- |
| 0x00000001 | Format Version                    | u32       |           |
| RANDOM     | Salt ⟳                            | bytes[32] |           |
| DEFINED    | Rounds for the KDF                | u64       |           |
| RANDOM     | IV ⟳                              | bytes[12] |           |
| 0x00       | Has compression                   | byte      |           |
| 1,048,576  | Encryption block size             | u32       |           |
| 0x00000000 | End of clear header               | u32       |           |
| DEFINED    | Entry table size (in items)       | u64       | Encrypted |
| DEFINED    | Start of the block stream (bytes) | u32       | Encrypted |
| DEFINED    | Number of blocks                  | u32       | Encrypted |
| DEFINED    | Size of the last block            | u32       | Encrypted |
| RANDOM     | SHA-256 hash of header            | i32       |           |

## Data table


Folder

| 0x01       | type (folder)                         | byte    |
| ---------- | ------------------------------------- | ------- |
| 0x00000008 | Name size                             | u32     |
| Grégoire   | Name                                  | bytes[] |
|            | size (of self)                        | u32     |
| DEFINED    | size (of items, bytes)                | u32     |
| DEFINED    | Start position (block)                | u32     |
| DEFINED    | Inner block padding                   | u32     |
| 0x00001100 | Color (6 bytes), importance (2 bytes) | u32     |
| DEFINED    | Monochrome icon (square matrix)       | bytes[] |

Entry (fixed size + VD)

| 0x02                    | type (entry)                          | byte    |          |
| ----------------------- | ------------------------------------- | ------- | -------- |
| 0x00000001              | Entry type                            | u32     |          |
| 0x00000006              | Name size                             | u32     |          |
| Fedora                  | Name                                  | bytes[] |          |
| 0x00001100              | Color (6 bytes), importance (2 bytes) | u32     |          |
| DEFINED                 | Monochrome icon (square matrix)       | bytes[] |          |
| DEFINED                 | Variant dictionary size               | u32     |          |
|                         | VARIANT DICTIONARY                    |         |          |
| 0x0000006F              | URL size                              | u32     | Specific |
| https://duckduckgo.com/ | URL                                   | bytes[] | Specific |
| 0x00000002              | Username size                         | u32     | Specific |
| me                      | Username                              | bytes[] | Specific |
| 0x000000F1              | Pass size                             | u32     | Specific |
| S3cur3 p4ssw0rd!        | Pass                                  | bytes[] | Specific |
| 0x00000000              | VD END                                | u32     |          |

Multiple type to be defined

## Stream block

Stream Block key : SHA-512(i ‖ SHA-512(S ‖ T ‖ 0x01))
Content key : SHA-256(S ‖ T)

Block protected with HMAC signature, encrypted with ChaCha20
Block size to be defined (1 Kb ?)

The HMAC-protected block stream is terminated by an output block for an empty input block (i.e. M empty, s = 0)

| RANDOM     | HMAC-SHA-256(i \|\| s \|\| M)           | u32     |
| ---------- | --------------------------------------- | ------- |
| 0x000F4240 | Size (here, 1MB)                        | u32     |
| DEFINED    | Content (Variant dictionnary, ChaCha20) | bytes[] |
