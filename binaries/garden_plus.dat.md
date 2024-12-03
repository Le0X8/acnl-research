# garden_plus.dat

All data types are little-endian.

## Overall structure

| Size      |
| --------- |
| `0x89b00` |

| Offset    | Size      | Type                          | Description |
| --------- | --------- | ----------------------------- | ----------- |
| `0x00000` | `0x00080` | [SecureValue](#securevalue)   |             |
|           |           | [SaveHeader](#saveheader)     |             |
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
