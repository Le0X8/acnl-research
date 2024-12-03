# garden_plus.dat

All data types are little-endian.

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

| Offset    | Size      | Type   | Description                     |
| --------- | --------- | ------ | ------------------------------- |
| `0x00000` | `0x00004` | u32    | CRC-32 of the next 28 bytes     |
| `0x00004` | `0x00002` | u16    | Save verifier 1 (always 158)    |
| `0x00006` | `0x00001` | u8     | Save verifier 2 (always 2) |
| `0x00007` | `0x00019` | u8[25] | Padding (always 0)              |

Used in:

- [Overall structure](#overall-structure)
