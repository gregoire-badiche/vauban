Projet
ESP32 WROVER or WROOM serie 
SPI Flash Winbond W25Q128
USB-to-UART chip (?)
Very small screen
Controller (need at least 4 directional arrows)

# File specs

## Algorithms

AES-KDF
ChaCha20
SHA-256
HMAC-SHA-256

## Header

Fixed size, Master key computed using AES-KDF with the IV and the number of round

Integers are stored in little-endian byte order, i.e. the least significant byte is stored first. For example, the integer 0x12345678 is stored as the byte sequence (0x78, 0x56, 0x34, 0x12)

| Data Example | Description                       | Data Type |
| ------------ | --------------------------------- | --------- |
| Ox76617562   | File signature                    | u32       |
| 0x00000001   | Format Version                    | u32       |
| RANDOM       | Salt ⟳                            | bytes[32] |
| DEFINED      | Rounds for the KDF                | u64       |
| RANDOM       | IV ⟳                              | bytes[12] |
| 0x00         | Has compression                   | byte      |
| 1,048,576    | Encryption block size             | u32       |
| DEFINED      | Number of blocks                  | u32       |
| 0x00000000   | End of clear header               | u32       |
| RANDOM       | SHA-256 hash of header            | i32       |

## Data table


Folder

| Data Example | Description                           | Data Type |
| ------------ | ------------------------------------- | --------- |
| 0x01         | type (folder)                         | byte      |
| 0x00000008   | Name size                             | u32       |
| Grégoire     | Name                                  | bytes[]   |
| DEFINED      | size (of self)                        | u32       |
| DEFINED      | size (of items, bytes)                | u32       |
| DEFINED      | Start position (block)                | u32       |
| DEFINED      | Inner block padding                   | u32       |
| 0x00001100   | Color (6 bytes), importance (2 bytes) | u32       |
| DEFINED      | Monochrome icon (square matrix)       | bytes[]   |

Entry (fixed size + Variant Dictionary)

| Data Example            | Description                           | Data Type |          |
| ----------------------- | ------------------------------------- | --------- | -------- |
| 0x02                    | type (entry)                          | byte      |          |
| 0x00000001              | Entry type                            | u32       |          |
| 0x00000006              | Name size                             | u32       |          |
| Fedora                  | Name                                  | bytes[]   |          |
| 0x00001100              | Color (6 bytes), importance (2 bytes) | u32       |          |
| DEFINED                 | Monochrome icon (square matrix)       | bytes[]   |          |
| DEFINED                 | Variant dictionary size               | u32       |          |
|                         | VARIANT DICTIONARY                    |           |          |
| 0x0000006F              | URL size                              | u32       | Specific |
| https://duckduckgo.com/ | URL                                   | bytes[]   | Specific |
| 0x00000002              | Username size                         | u32       | Specific |
| me                      | Username                              | bytes[]   | Specific |
| 0x000000F1              | Pass size                             | u32       | Specific |
| S3cur3 p4ssw0rd!        | Pass                                  | bytes[]   | Specific |
| 0x00000000              | Variant Dictionary END                | u32       |          |

Multiple types to be defined

## Stream block

Stream Block key : SHA-512(i ‖ SHA-512(S ‖ T ‖ 0x01))
Content key : SHA-256(S ‖ T)

Block protected with HMAC signature, encrypted with ChaCha20
Block size to be defined (1 Kb ?)

The HMAC-protected block stream is terminated by an output block for an empty input block (i.e. M empty, s = 0)

| Data Example | Description                             | Data Type |
| ------------ | --------------------------------------- | --------- |
| RANDOM       | HMAC-SHA-256(i \|\| s \|\| M)           | u32       |
| 0x000F4240   | Size (here, 1MB)                        | u32       |
| DEFINED      | Content (Variant dictionnary, ChaCha20) | bytes[]   |
