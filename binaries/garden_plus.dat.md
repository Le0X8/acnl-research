# garden_plus.dat

All data types are little-endian. Strings are null-terminated and UTF-16LE encoded.

## Overall structure

| Size      |
| --------- |
| `0x89b00` |

| Offset    | Size      | Type                          | Description |
| --------- | --------- | ----------------------------- | ----------- |
| `0x00000` | `0x00080` | [SecureValue](#securevalue)   |             |
| `0x00080` | `0x00020` | [SaveHeader](#saveheader)     |             |
|           |           | [Player](#player)[4]          |             |
|           |           | [VillagerData](#villagerdata) |             |
|           |           | [BuildingData](#buildingdata) |             |
|           |           | [MinigameData](#minigamedata) |             |
|           |           | [UnknownData](#unknowndata)   |             |
|           |           | [TownData](#towndata)         |             |

## Data types

### SecureValue

| Size      |
| --------- |
| `0x00080` |

| Offset    | Size      | Type    | Description                                              |
| --------- | --------- | ------- | -------------------------------------------------------- |
| `0x00000` | `0x00008` | u64     | Value for the game to determine if the savegame is legit |
| `0x00008` | `0x00004` | u32     | Game initialized? (has to be 1)                          |
| `0x0000c` | `0x00074` | u8[116] | Padding (always 0)                                       |

Used in:

- [Overall structure](#overall-structure)

### SaveHeader

| Size      |
| --------- |
| `0x00020` |

| Offset    | Size      | Type   | Description                  |
| --------- | --------- | ------ | ---------------------------- |
| `0x00000` | `0x00004` | u32    | CRC-32 of the next 28 bytes  |
| `0x00004` | `0x00002` | u16    | Save verifier 1 (always 158) |
| `0x00006` | `0x00001` | u8     | Save verifier 2 (always 2)   |
| `0x00007` | `0x00019` | u8[25] | Padding (always 0)           |

Used in:

- [Overall structure](#overall-structure)

### Player

| Size      |
| --------- |
| `0x00000` |

| Offset    | Size      | Type                    | Description                    |
| --------- | --------- | ----------------------- | ------------------------------ |
| `0x00000` | `0x00004` | u32                     | CRC-32 of the next 27524 bytes |
| `0x00004` | `0x00001` | u8                      | Hair style                     |
| `0x00005` | `0x00001` | u8                      | Hair color                     |
| `0x00006` | `0x00001` | u8                      | Face                           |
| `0x00007` | `0x00001` | u8                      | Eye color                      |
| `0x00008` | `0x00002` | u16                     | Tan                            |
| `0x0000a` | `0x00004` | [Item](#item)           | Hat                            |
| `0x0000e` | `0x00004` | [Item](#item)           | Accessory                      |
| `0x00012` | `0x00004` | [Item](#item)           | Top wear                       |
| `0x00016` | `0x00004` | [Item](#item)           | Under-top wear                 |
| `0x0001a` | `0x00004` | [Item](#item)           | Bottom wear                    |
| `0x0001e` | `0x00004` | [Item](#item)           | Socks                          |
| `0x00022` | `0x00004` | [Item](#item)           | Shoes                          |
| `0x00026` | `0x00004` | [Item](#item)           | Equipped item                  |
| `0x0002a` | `0x00001` | u8                      | ?                              |
| `0x0002b` | `0x00001` | u8                      | Padding (always 0)             |
| `0x0002c` | `0x05460` | [Pattern](#pattern)[10] | Player design patterns         |
| `0x0548c` | `0x0000a` | u8[10]                  | Player design order (0-9)      |
| `0x05496` | `0x00002` | u16                     | Padding (always 0)             |
| `0x05498` | `0x00000` | ?                       | TODO                           |

Used in:

- [Overall structure](#overall-structure)

## Item

| Size      |
| --------- |
| `0x00004` |

| Offset    | Size      | Type | Description |
| --------- | --------- | ---- | ----------- |
| `0x00000` | `0x00002` | u16  | Item ID     |
| `0x00002` | `0x00001` | u8   | Item flag 1 |
| `0x00003` | `0x00001` | u8   | Item flag 2 |

Used in:

- [Player](#player)

## Pattern

| Size      |
| --------- |
| `0x00870` |

| Offset    | Size      | Type                      | Description                    |
| --------- | --------- | ------------------------- | ------------------------------ |
| `0x00000` | `0x0002a` | str                       | Design name                    |
| `0x0002a` | `0x0002e` | [PersonalId](#personalid) | Creator                        |
| `0x00058` | `0x0000f` | u8[15]                    | Color palette                  |
| `0x00067` | `0x00001` | u8                        | ?                              |
| `0x00068` | `0x00001` | u8                        | ? (always 10)                  |
| `0x00069` | `0x00001` | u8                        | [Pattern type](#pattern-types) |
| `0x0006a` | `0x00002` | u16                       | Padding (always 0)             |
| `0x0006c` | `0x00200` | u8[512]                   | Design data 1                  |
| `0x0026c` | `0x00200` | u8[512]                   | Design data 2 (PRO only)       |
| `0x0046c` | `0x00200` | u8[512]                   | Design data 3 (PRO only)       |
| `0x0066c` | `0x00200` | u8[512]                   | Design data 4 (PRO only)       |
| `0x0086c` | `0x00004` | u32                       | Padding (always 0)             |

Used in:

- [Player](#player)

### Pattern types

| Value  | Description        |
| ------ | ------------------ |
| `0x00` | Long sleeve dress  |
| `0x01` | Short sleeve dress |
| `0x02` | Sleeveless dress   |
| `0x03` | Long sleeve shirt  |
| `0x04` | Short sleeve shirt |
| `0x05` | Sleeveless shirt   |
| `0x06` | Horned hat         |
| `0x07` | Knit hat           |
| `0x08` | Photo board        |
| `0x09` | Normal pattern     |

## PersonalId

| Size      |
| --------- |
| `0x0002e` |

| Offset    | Size      | Type              | Description        |
| --------- | --------- | ----------------- | ------------------ |
| `0x00000` | `0x00002` | u16               | Player ID          |
| `0x00002` | `0x00012` | str               | Player name        |
| `0x00014` | `0x00001` | u8                | Gender             |
| `0x00015` | `0x00001` | u8                | Padding (always 0) |
| `0x00016` | `0x00016` | [TownId](#townid) | Hometown           |
| `0x0002c` | `0x00001` | u8                | TPC State          |
| `0x0002d` | `0x00001` | u8                | TPC Region         |

Used in:

- [Pattern](#pattern)

## TownId

| Size      |
| --------- |
| `0x00016` |

| Offset    | Size      | Type | Description |
| --------- | --------- | ---- | ----------- |
| `0x00000` | `0x00002` | u16  | Town ID     |
| `0x00002` | `0x00012` | str  | Town name   |
| `0x00014` | `0x00001` | u8   | ?           |
| `0x00015` | `0x00001` | u8   | ?           |

Used in:

- [PersonalId](#personalid)
