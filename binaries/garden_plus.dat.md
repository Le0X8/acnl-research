# garden_plus.dat

All data types are little-endian. Strings are null-terminated and UTF-16LE encoded.

## Overall structure

| Size      |
| --------- |
| `0x89b00` |

| Offset    | Size      | Type                          | Description | JSON key       |
| --------- | --------- | ----------------------------- | ----------- | -------------- |
| `0x00000` | `0x00080` | [SecureValue](#securevalue)   |             | `securevalue`  |
| `0x00080` | `0x00020` | [SaveHeader](#saveheader)     |             | `saveheader`   |
| `0x000a0` | `0x29200` | [Player](#player)[4]          |             | `players[]`    |
| `0x292a0` | `0x22be0` | [VillagerData](#villagerdata) |             | `villagerData` |
| `0x4be80` | `0x044bc` | [BuildingData](#buildingdata) |             | `buildingData` |
| `0x5033c` | `0x028f4` | [MinigameData](#minigamedata) |             | `minigameData` |
| `0x52c30` | `0x007f4` | [UnknownData](#unknowndata)   |             | `unknownData`  |
| `0x53424` | `0x366dc` | [TownData](#towndata)         |             | `townData`     |

## SecureValue

| Size      |
| --------- |
| `0x00080` |

| Offset    | Size      | Type    | Description                                              | JSON key      |
| --------- | --------- | ------- | -------------------------------------------------------- | ------------- |
| `0x00000` | `0x00008` | u64     | Value for the game to determine if the savegame is legit | `signature`   |
| `0x00008` | `0x00004` | u32     | Game initialized? (has to be 1)                          | `initialized` |
| `0x0000c` | `0x00074` | u8[116] | Padding (always 0)                                       | `padding`     |

Used in:

- [Overall structure](#overall-structure)

## SaveHeader

| Size      |
| --------- |
| `0x00020` |

| Offset    | Size      | Type   | Description                  | JSON key    |
| --------- | --------- | ------ | ---------------------------- | ----------- |
| `0x00000` | `0x00004` | u32    | CRC-32 of the next 28 bytes  | `crc32`     |
| `0x00004` | `0x00002` | u16    | Save verifier 1 (always 158) | `verifier1` |
| `0x00006` | `0x00001` | u8     | Save verifier 2 (always 2)   | `verifier2` |
| `0x00007` | `0x00019` | u8[25] | Padding (always 0)           | `padding`   |

Used in:

- [Overall structure](#overall-structure)

## Player

| Size      |
| --------- |
| `0x0a480` |

| Offset    | Size      | Type                              | Description                                         | JSON key            |
| --------- | --------- | --------------------------------- | --------------------------------------------------- | ------------------- |
| `0x00000` | `0x00004` | u32                               | CRC-32 of the next 27524 bytes                      | `crc32`             |
| `0x00004` | `0x00001` | u8                                | Hair style                                          | `hairStyle`         |
| `0x00005` | `0x00001` | u8                                | Hair color                                          | `hairColor`         |
| `0x00006` | `0x00001` | u8                                | Face                                                | `face`              |
| `0x00007` | `0x00001` | u8                                | Eye color                                           | `eyeColor`          |
| `0x00008` | `0x00002` | u16                               | Tan                                                 | `tan`               |
| `0x0000a` | `0x00004` | [Item](#item)                     | Hat                                                 | `hat`               |
| `0x0000e` | `0x00004` | [Item](#item)                     | Accessory                                           | `accessory`         |
| `0x00012` | `0x00004` | [Item](#item)                     | Top wear                                            | `topWear`           |
| `0x00016` | `0x00004` | [Item](#item)                     | Under-top wear                                      | `underTopWear`      |
| `0x0001a` | `0x00004` | [Item](#item)                     | Bottom wear                                         | `bottomWear`        |
| `0x0001e` | `0x00004` | [Item](#item)                     | Socks                                               | `socks`             |
| `0x00022` | `0x00004` | [Item](#item)                     | Shoes                                               | `shoes`             |
| `0x00026` | `0x00004` | [Item](#item)                     | Equipped item                                       | `equippedItem`      |
| `0x0002a` | `0x00001` | u8                                | ?                                                   | `unknown0x0002a`    |
| `0x0002b` | `0x00001` | u8                                | Padding (always 0)                                  | `padding0x0002b`    |
| `0x0002c` | `0x05460` | [Pattern](#pattern)[10]           | Player design patterns                              | `patterns`          |
| `0x0548c` | `0x0000a` | u8[10]                            | Player design order (0-9)                           | `patternOrder`      |
| `0x05496` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x05496`    |
| `0x05498` | `0x000a8` | [MiiData](#miidata)               | Mii data                                            | `miiData`           |
| `0x05540` | `0x00001` | bool                              | Has Mii?                                            | `hasMii`            |
| `0x05541` | `0x00001` | u8                                | ?                                                   | `unknown0x05541`    |
| `0x05542` | `0x00002` | u16                               | ?                                                   | `unknown0x05542`    |
| `0x05544` | `0x00060` | [Mannequin](#mannequin)[4]        | Player mannequins                                   | `mannequins`        |
| `0x055a4` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x055a4`    |
| `0x055a6` | `0x0002e` | [PersonalId](#personalid)         | Player info                                         | `personalId`        |
| `0x055d4` | `0x00001` | u8                                | Birth month                                         | `birthMonth`        |
| `0x055d5` | `0x00001` | u8                                | Birth day                                           | `birthDay`          |
| `0x055d6` | `0x00002` | u16                               | Registration year                                   | `registrationYear`  |
| `0x055d8` | `0x00001` | u8                                | Registration month                                  | `registrationMonth` |
| `0x055d9` | `0x00001` | u8                                | Registration day                                    | `registrationDay`   |
| `0x055da` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x055da`    |
| `0x055dc` | `0x000e8` | [PlayerBadges](#playerbadges)     | Player badges                                       | `playerBadges`      |
| `0x056c4` | `0x0002c` | [HhaHouseInfo](#hhahouseinfo)     | HHA house info                                      | `hhaHouseInfo`      |
| `0x056f0` | `0x0000c` | [DreamAddress](#dreamaddress)     | Dream address                                       | `dreamAddress`      |
| `0x056fc` | `0x00004` | u32                               | Padding (always 0)                                  | `padding0x056fc`    |
| `0x05700` | `0x00034` | u8[52]                            | ?                                                   | `unknown0x05700`    |
| `0x05734` | `0x00004` | u32                               | Has TPC pic?                                        | `hasTpcPic`         |
| `0x05738` | `0x01400` | u8[5120]                          | TPC pic (JPEG)                                      | `tpcPic`            |
| `0x06b38` | `0x00042` | str                               | TPC text                                            | `tpcText`           |
| `0x06b7a` | `0x00001` | u8                                | ?                                                   | `unknown0x06b7a`    |
| `0x06b7b` | `0x00001` | u8                                | ?                                                   | `unknown0x06b7b`    |
| `0x06b7c` | `0x00004` | u32                               | ?                                                   | `unknown0x06b7c`    |
| `0x06b80` | `0x00004` | u32                               | ?                                                   | `unknown0x06b80`    |
| `0x06b84` | `0x00004` | u32                               | Padding (always 0)                                  | `padding0x06b84`    |
| `0x06b88` | `0x00004` | u32                               | CRC-32 of the next 13220 bytes                      | `crc32_2`           |
| `0x06b8c` | `0x00008` | [EncryptedValue](#encryptedvalue) | Amount of bells in bank                             | `bank`              |
| `0x06b94` | `0x00008` | [EncryptedValue](#encryptedvalue) | Remaining debt                                      | `bank`              |
| `0x06b9c` | `0x00008` | [EncryptedValue](#encryptedvalue) | Island medals                                       | `medals`            |
| `0x06ba4` | `0x00008` | [EncryptedValue](#encryptedvalue) | Amount of bells received from Reese                 | `bellsFromReese`    |
| `0x06bac` | `0x00004` | u32                               | Padding (always 0)                                  | `padding0x06ba4`    |
| `0x06bb0` | `0x00008` | u64                               | Playtime                                            | `playtime`          |
| `0x06bb8` | `0x00016` | [TownId](#townid)                 | Town ID                                             | `townId`            |
| `0x06bce` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x06bc6`    |
| `0x06bd0` | `0x00040` | [Item](#item)[16]                 | Inventory                                           | `inventory`         |
| `0x06c10` | `0x00010` | u8[16]                            | Inventory item locks                                | `inventoryLocks`    |
| `0x06c20` | `0x002e8` | u8[744]                           | Unlocked items                                      | `unlockedItems`     |
| `0x06f08` | `0x00008` | [EncryptedValue](#encryptedvalue) | Amount of bells in wallet                           | `wallet`            |
| `0x06f10` | `0x000a0` | [Item](#item)[40]                 | Island box items                                    | `islandBox`         |
| `0x06fb0` | `0x00040` | [Item](#item)[16]                 | Island inventory                                    | `islandInventory`   |
| `0x06ff0` | `0x00010` | u8[16]                            | ?                                                   | `unknown0x06ff0`    |
| `0x07000` | `0x00004` | [Item](#item)                     | ?                                                   | `unknown0x07000`    |
| `0x07004` | `0x00004` | [Item](#item)                     | ?                                                   | `unknown0x07004`    |
| `0x07008` | `0x01900` | [Letter](#letter)[10]             | Player inventory letters                            | `playerLetters`     |
| `0x08908` | `0x00040` | str                               | Last used letter header                             | `lastLetterHeader`  |
| `0x08948` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x08948`    |
| `0x0894a` | `0x00040` | str                               | Last used "Future me" letter header                 | `lastFutureMe`      |
| `0x0898a` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x0898a`    |
| `0x0898c` | `0x00040` | str                               | Last used letter footer                             | `lastLetterFooter`  |
| `0x089cc` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x089cc`    |
| `0x089ce` | `0x00001` | u8                                | Last used letter receiver name position             | `lastReceiverPos`   |
| `0x089cf` | `0x00001` | u8                                | Last used letter receiver name position (Future me) | `lastFutureMePos`   |
| `0x089d0` | `0x00028` | u8[40]                            | Player emote slots                                  | `emotes`            |
| `0x089f8` | `0x00001` | i8                                | Current emote page (-1: page 1, 0: page 2)          | `emotePage`         |
| `0x089f9` | `0x00001` | u8                                | Padding (always 0)                                  | `padding0x089f9`    |
| `0x089fa` | `0x00040` | u16[32]                           | ?                                                   | `unknown0x089fa`    |
| `0x08a3a` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x08a3a`    |
| `0x08a3c` | `0x00080` | u8[128]                           | ?                                                   | `unknown0x08a3c`    |
| `0x08abc` | `0x00002` | u16                               | Padding (always 0)                                  | `padding0x08abc`    |
| `0x08abe` | `0x00001` | u8                                | Lyle flags                                          | `lyleFlags`         |
| `0x08abf` | `0x0025d` | u8[605]                           | ?                                                   | `unknown0x08abf`    |
| `0x08d1c` | `0x00008` | [EncryptedValue](#encryptedvalue) | MEOW coupons                                        | `meowCoupons`       |
| `0x08d24` | `0x00008` | [EncryptedValue](#encryptedvalue) | ?                                                   | `unknown0x08d24`    |
| `0x08d2c` | `0x00008` | [EncryptedValue](#encryptedvalue) | ?                                                   | `unknown0x08d2c`    |
| `0x08d34` | `0x00008` | [EncryptedValue](#encryptedvalue) | ?                                                   | `unknown0x08d34`    |
| `0x08d3c` | `0x00008` | [EncryptedValue](#encryptedvalue) | ?                                                   | `unknown0x08d3c`    |
| `0x08d44` | `0x00008` | [EncryptedValue](#encryptedvalue) | ?                                                   | `unknown0x08d44`    |
| `0x08d4c` | `0x0025c` | u8[604]                           | ?                                                   | `unknown0x08d4c`    |
| `0x08fa8` | `0x00028` | [Item](#item)[10]                 | Santa bag inventory                                 | `santaBag`          |
| `0x08fd0` | `0x00320` | u8[800]                           | ?                                                   | `unknown0x08fd0`    |
| `0x092f0` | `0x002d0` | [Item](#item)[180]                | Player dressers                                     | `dressers`          |
| `0x095c0` | `0x00044` | str                               | Birthday wish                                       | `birthdayWish`      |
| `0x09604` | `0x00c80` | [Letter](#letter)[5]              | ?                                                   | `unknown0x09604`    |
| `0x0a284` | `0x001fc` | u8[508]                           | ?                                                   | `unknown0x0a284`    |

Used in:

- [Overall structure](#overall-structure)

## Item

| Size      |
| --------- |
| `0x00004` |

| Offset    | Size      | Type | Description | JSON key |
| --------- | --------- | ---- | ----------- | -------- |
| `0x00000` | `0x00002` | u16  | Item ID     | `id`     |
| `0x00002` | `0x00001` | u8   | Item flag 1 | `flag1`  |
| `0x00003` | `0x00001` | u8   | Item flag 2 | `flag2`  |

Used in:

- [Player](#player)
- [Mannequin](#mannequin)
- [Letter](#letter)

## Pattern

| Size      |
| --------- |
| `0x00870` |

| Offset    | Size      | Type                      | Description                    | JSON key         |
| --------- | --------- | ------------------------- | ------------------------------ | ---------------- |
| `0x00000` | `0x0002a` | str                       | Design name                    | `name`           |
| `0x0002a` | `0x0002e` | [PersonalId](#personalid) | Creator                        | `creator`        |
| `0x00058` | `0x0000f` | u8[15]                    | Color palette                  | `colorPalette`   |
| `0x00067` | `0x00001` | u8                        | ?                              | `unknown0x00067` |
| `0x00068` | `0x00001` | u8                        | ? (always 10)                  | `unknown0x00068` |
| `0x00069` | `0x00001` | u8                        | [Pattern type](#pattern-types) | `type`           |
| `0x0006a` | `0x00002` | u16                       | Padding (always 0)             | `padding0x0006a` |
| `0x0006c` | `0x00200` | u8[512]                   | Design data 1                  | `designData1`    |
| `0x0026c` | `0x00200` | u8[512]                   | Design data 2 (PRO only)       | `designData2`    |
| `0x0046c` | `0x00200` | u8[512]                   | Design data 3 (PRO only)       | `designData3`    |
| `0x0066c` | `0x00200` | u8[512]                   | Design data 4 (PRO only)       | `designData4`    |
| `0x0086c` | `0x00004` | u32                       | Padding (always 0)             | `padding0x0086c` |

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

| Offset    | Size      | Type              | Description        | JSON key         |
| --------- | --------- | ----------------- | ------------------ | ---------------- |
| `0x00000` | `0x00002` | u16               | Player ID          | `id`             |
| `0x00002` | `0x00012` | str               | Player name        | `name`           |
| `0x00014` | `0x00001` | u8                | Gender             | `gender`         |
| `0x00015` | `0x00001` | u8                | Padding (always 0) | `padding0x00015` |
| `0x00016` | `0x00016` | [TownId](#townid) | Hometown           | `hometown`       |
| `0x0002c` | `0x00001` | u8                | TPC State          | `tpcState`       |
| `0x0002d` | `0x00001` | u8                | TPC Region         | `tpcRegion`      |

Used in:

- [Pattern](#pattern)
- [Player](#player)
- [Letter](#letter)

## TownId

| Size      |
| --------- |
| `0x00016` |

| Offset    | Size      | Type | Description | JSON key      |
| --------- | --------- | ---- | ----------- | ------------- |
| `0x00000` | `0x00002` | u16  | Town ID     | `id`          |
| `0x00002` | `0x00012` | str  | Town name   | `name`        |
| `0x00014` | `0x00001` | u8   | ?           | `unknown0x14` |
| `0x00015` | `0x00001` | u8   | ?           | `unknown0x15` |

Used in:

- [PersonalId](#personalid)
- [Player](#player)
- [Villager](#villager)

## MiiData

| Size      |
| --------- |
| `0x000a8` |

| Offset    | Size      | Type   | Description                                              | JSON key         |
| --------- | --------- | ------ | -------------------------------------------------------- | ---------------- |
| `0x00000` | `0x0005c` | u8[92] | Face data (see <https://3dbrew.org/wiki/Mii#Mii_format>) | `faceData`       |
| `0x0005c` | `0x00002` | u16    | Padding (always 0)                                       | `padding0x0005c` |
| `0x0005e` | `0x00002` | u16    | Mii face data CRC-16                                     | `faceDataCrc16`  |
| `0x00060` | `0x00010` | u32[4] | AES_CCM_MAC                                              | `aesCcmMac`      |
| `0x00070` | `0x00018` | u8[24] | Unknown data                                             | `unknownData`    |
| `0x00088` | `0x0001e` | u8[30] | Padding (always 0)                                       | `padding0x00088` |
| `0x000a6` | `0x00002` | u16    | Padding (always 0)                                       | `padding0x000a6` |

Used in:

- [Player](#player)

## Mannequin

| Size      |
| --------- |
| `0x00018` |

| Offset    | Size      | Type          | Description | JSON key     |
| --------- | --------- | ------------- | ----------- | ------------ |
| `0x00000` | `0x00004` | [Item](#item) | Hat         | `hat`        |
| `0x00004` | `0x00004` | [Item](#item) | Accessory   | `accessory`  |
| `0x00008` | `0x00004` | [Item](#item) | Top wear    | `topWear`    |
| `0x0000c` | `0x00004` | [Item](#item) | Bottom wear | `bottomWear` |
| `0x00010` | `0x00004` | [Item](#item) | Socks       | `socks`      |
| `0x00014` | `0x00004` | [Item](#item) | Shoes       | `shoes`      |

Used in:

- [Player](#player)

## PlayerBadges

| Size      |
| --------- |
| `0x000e8` |

| Offset    | Size      | Type                                  | Description  | JSON key         |
| --------- | --------- | ------------------------------------- | ------------ | ---------------- |
| `0x00000` | `0x000c0` | [EncryptedValue](#encryptedvalue)[24] | Badge values | `badgeValues`    |
| `0x000c0` | `0x00018` | u8[24]                                | Badges       | `badges`         |
| `0x000d8` | `0x00008` | [EncryptedValue](#encryptedvalue)     | ?            | `unknown0x000d8` |
| `0x000e0` | `0x00008` | [EncryptedValue](#encryptedvalue)     | ?            | `unknown0x000e0` |

Used in:

- [Player](#player)

## EncryptedValue

| Size      |
| --------- |
| `0x00008` |

`// TODO`

Used in:

- [PlayerBadges](#playerbadges)

## HhaHouseInfo

| Size      |
| --------- |
| `0x0002c` |

| Offset    | Size      | Type   | Description                   |
| --------- | --------- | ------ | ----------------------------- |
| `0x00000` | `0x00004` | i32    | HHA house points              |
| `0x00004` | `0x0000a` | u16[5] | HHA items                     |
| `0x0000e` | `0x00002` | u16    | Exterior item                 |
| `0x00010` | `0x00002` | u16    | Interior item                 |
| `0x00012` | `0x00002` | u16    | HHA item                      |
| `0x00014` | `0x00001` | u8     | Current house theme           |
| `0x00015` | `0x00001` | u8     | Evaluation type               |
| `0x00016` | `0x0000b` | u8[11] | ?                             |
| `0x00021` | `0x00001` | u8     | Exterior obeying theme? (0-5) |
| `0x00022` | `0x00001` | u8     | Interior obeying theme? (0-5) |
| `0x00023` | `0x00001` | u8     | Impressive floor (0-5)        |
| `0x00024` | `0x00002` | u8[2]  | ?                             |
| `0x00026` | `0x00001` | u8     | Future advice (0-10)          |
| `0x00027` | `0x00001` | u8     | HHA awards unlocked (0-8)     |
| `0x00028` | `0x00001` | u8     | HHA awards received (0-8)     |
| `0x00029` | `0x00001` | u8     | Gold exteriors unlocked (0-5) |
| `0x0002a` | `0x00001` | u8     | Gold exteriors applied (0-5)  |
| `0x0002b` | `0x00001` | u8     | ?                             |

Used in:

- [Player](#player)

## DreamAddress

| Size      |
| --------- |
| `0x0000c` |

| Offset    | Size      | Type | Description       | JSON key        |
| --------- | --------- | ---- | ----------------- | --------------- |
| `0x00000` | `0x00004` | u32  | Dream code part 1 | `dreamCode1`    |
| `0x00004` | `0x00004` | u32  | Dream code part 2 | `dreamCode2`    |
| `0x00008` | `0x00001` | u8   | ?                 | `unknown0x0008` |
| `0x00009` | `0x00001` | u8   | Dream code part 3 | `dreamCode3`    |
| `0x0000a` | `0x00002` | u16  | Padding           | `padding0x000a` |

Used in:

- [Player](#player)

## Letter

| Size      |
| --------- |
| `0x00280` |

| Offset    | Size      | Type                      | Description                                                               | JSON key          |
| --------- | --------- | ------------------------- | ------------------------------------------------------------------------- | ----------------- |
| `0x00000` | `0x0002e` | [PersonalId](#personalid) | Receiver                                                                  | `receiver`        |
| `0x0002e` | `0x00002` | u16                       | Padding                                                                   | `padding0x0002e`  |
| `0x00030` | `0x00002` | u16                       | ?                                                                         | `unknown0x00030`  |
| `0x00032` | `0x00032` | u8[50]                    | Padding                                                                   | `padding0x00032`  |
| `0x00064` | `0x00002` | u16                       | ?                                                                         | `unknown0x00064`  |
| `0x00066` | `0x00002` | u16                       | Padding                                                                   | `padding0x00066`  |
| `0x00068` | `0x00040` | str                       | Letter header                                                             | `header`          |
| `0x000a8` | `0x00002` | u16                       | Padding                                                                   | `padding0x000a8`  |
| `0x000aa` | `0x00180` | str                       | Letter body                                                               | `body`            |
| `0x0022a` | `0x00002` | u16                       | Padding                                                                   | `padding0x0022a`  |
| `0x0022c` | `0x00040` | str                       | Letter footer                                                             | `footer`          |
| `0x0026c` | `0x00002` | u16                       | Padding                                                                   | `padding0x0026c`  |
| `0x0026e` | `0x00001` | u8                        | Receiver name position (in letter header, gets inserted at this position) | `receiverNamePos` |
| `0x0026f` | `0x00001` | u8                        | Paper type                                                                | `paperType`       |
| `0x00270` | `0x00001` | u8                        | ?                                                                         | `unknown0x00270`  |
| `0x00271` | `0x00001` | u8                        | ?                                                                         | `unknown0x00271`  |
| `0x00272` | `0x00001` | u8                        | Letter type                                                               | `type`            |
| `0x00273` | `0x00001` | u8                        | ?                                                                         | `unknown0x00273`  |
| `0x00274` | `0x00004` | [Item](#item)             | Present                                                                   | `present`         |
| `0x00278` | `0x00008` | u64                       | ?                                                                         | `unknown0x00278`  |

Used in:

- [Player](#player)

## VillagerData

| Size      |
| --------- |
| `0x22be0` |

| Offset    | Size      | Type                      | Description                     | JSON key         |
| --------- | --------- | ------------------------- | ------------------------------- | ---------------- |
| `0x00000` | `0x00004` | u32                       | CRC-32 of the next 142280 bytes | `crc32`          |
| `0x00004` | `0x172f0` | [Villager](#villager)[10] | Villagers                       | `villagers`      |
| `0x172f4` | `0x02478` | u8[9336]                  | ?                               | `unknown0x172f4` |
| `0x1976c` | `0x09460` | [Villager](#villager)[4]  | ?                               | `unknown0x1976c` |
| `0x22bcc` | `0x00014` | u8[20]                    | ?                               | `unknown0x22bcc` |

Used in:

- [Overall structure](#overall-structure)

## Villager

| Size      |
| --------- |
| `0x02518` |

| Offset    | Size      | Type                              | Description          | JSON key         |
| --------- | --------- | --------------------------------- | -------------------- | ---------------- |
| `0x00000` | `0x00016` | [TownId](#townid)                 | ?                    | `unknown0x00000` |
| `0x00016` | `0x00016` | [TownId](#townid)                 | ?                    | `unknown0x00016` |
| `0x0002c` | `0x00002` | u16                               | Villager ID          | `id`             |
| `0x0002e` | `0x00001` | u8                                | Villager personality | `personality`    |
| `0x0002f` | `0x00001` | u8                                | Padding (always 0)   | `padding0x0002f` |
| `0x00030` | `0x00870` | [Pattern](#pattern)               | Some kind of pattern | `pattern`        |
| `0x008a0` | `0x00016` | [TownId](#townid)                 | ?                    | `unknown0x008a0` |
| `0x008b6` | `0x00010` | u8[16]                            | ?                    | `unknown0x008b6` |
| `0x008c6` | `0x00028` | [Item](#item)[10]                 | ?                    | `unknown0x008c6` |
| `0x008ee` | `0x00f20` | [VillagerHome](#villagerhome)[16] | Villager homes       | `homes`          |
| `0x0180e` | `0x00002` | u16                               | Padding (always 0)   | `padding0x0180e` |
| `0x01810` | `0x00c80` | [Letter](#letter)[5]              | Letters              | `letters`        |
| `0x02490` | `0x0000a` | u16[5]                            | ?                    | `unknown0x02490` |
| `0x0249a` | `0x00004` | [Item](#item)                     | Shirt                | `shirt`          |
| `0x0249e` | `0x00004` | [Item](#item)                     | Song                 | `song`           |
| `0x024a2` | `0x00004` | [Item](#item)                     | Wallpaper            | `wallpaper`      |
| `0x024a6` | `0x00004` | [Item](#item)                     | Floor                | `floor`          |
| `0x024aa` | `0x00004` | [Item](#item)                     | Umbrella             | `umbrella`       |
| `0x024ae` | `0x00040` | [Item](#item)[16]                 | Furniture            | `furniture`      |
| `0x024ee` | `0x00004` | [Date](#date)                     | ?                    | `unknown0x024ee` |
| `0x024f2` | `0x00016` | str                               | Catchphrase          | `catchphrase`    |
| `0x02508` | `0x00002` | u8[2]                             | ?                    | `unknown0x02508` |
| `0x0250a` | `0x00004` | [Date](#date)                     | ?                    | `unknown0x0250a` |
| `0x0250e` | `0x00002` | u8[2]                             | ?                    | `unknown0x0250e` |
| `0x02510` | `0x00008` | u32[2]                            | ?                    | `unknown0x02510` |

Used in:

- [VillagerData](#villagerdata)

## VillagerHome

| Size      |
| --------- |
| `0x000f2` |

| Offset    | Size      | Type                      | Description | JSON key         |
| --------- | --------- | ------------------------- | ----------- | ---------------- |
| `0x00000` | `0x0002e` | [PersonalId](#personalid) | ?           | `unknown0x00000` |
| `0x0002e` | `0x00022` | u8[34]                    | ?           | `unknown0x0002e` |
| `0x00050` | `0x00012` | str                       | ?           | `unknown0x00050` |
| `0x00062` | `0x00054` | [Item](#item)[21]         | ?           | `unknown0x00062` |
| `0x000b6` | `0x0000a` | u8[10]                    | ?           | `unknown0x000b6` |
| `0x000c0` | `0x00016` | [TownId](#townid)         | ?           | `unknown0x000c0` |
| `0x000d6` | `0x00008` | u8[8]                     | ?           | `unknown0x000d6` |
| `0x000de` | `0x00010` | [Date](#date)[4]          | ?           | `unknown0x000de` |
| `0x000ee` | `0x00003` | u8[3]                     | ?           | `unknown0x000ee` |
| `0x000f1` | `0x00001` | u8                        | Padding     | `padding0x000f1` |

Used in:

- [Villager](#villager)

## Date

| Size      |
| --------- |
| `0x00004` |

| Offset    | Size      | Type | Description | JSON key |
| --------- | --------- | ---- | ----------- | -------- |
| `0x00000` | `0x00002` | u16  | Year        | `year`   |
| `0x00002` | `0x00001` | u8   | Month       | `month`  |
| `0x00003` | `0x00001` | u8   | Day         | `day`    |

Used in:

- [VillagerHome](#villagerhome)

## BuildingData

| Size      |
| --------- |
| `0x044bc` |

| Offset    | Size      | Type                           | Description                       | JSON key           |
| --------- | --------- | ------------------------------ | --------------------------------- | ------------------ |
| `0x00000` | `0x00004` | u32                            | Checksum of the next 0x44b8 bytes | `checksum`         |
| `0x00004` | `0x00001` | u8                             | Amount of normal PWPs             | `normalPWPsAmount` |
| `0x00005` | `0x00001` | u8                             | mount of event PWPs               | `eventPWPsAmount`  |
| `0x00006` | `0x00001` | u8                             | Town tree size (1-7)              | `townTreeSize`     |
| `0x00007` | `0x00001` | u8                             | Padding (always 0)                | `padding1`         |
| `0x00008` | `0x000e0` | [Building](#building)[56]      | Town buildings                    | `buildings`        |
| `0x000e8` | `0x00008` | [Building](#building)[2]       | Event buildings                   | `eventBuildings`   |
| `0x000f0` | `0x03b48` | [DesignStand](#designstand)[7] | Design stand related data         | `designStands`     |
| `0x03c38` | `0x00870` | [Pattern](#pattern)            | Unknown pattern                   | `unknownPattern1`  |
| `0x044a8` | `0x00014` | u8[20]                         | Unlocked PWPs (bitmap)            | `unlockedPWPs`     |

## Building

| Size      |
| --------- |
| `0x00004` |

| Offset    | Size      | Type | Description | JSON key |
| --------- | --------- | ---- | ----------- | -------- |
| `0x00000` | `0x00002` | u16  | Building ID | `id`     |
| `0x00002` | `0x00001` | u8   | X position  | `x`      |
| `0x00003` | `0x00001` | u8   | Y position  | `y`      |

## DesignStand

| Size      |
| --------- |
| `0x00878` |

| Offset    | Size      | Type                | Description | JSON key   |
| --------- | --------- | ------------------- | ----------- | ---------- |
| `0x00000` | `0x00870` | [Pattern](#pattern) | Design      | `design`   |
| `0x00870` | `0x00001` | u8                  | X position  | `x`        |
| `0x00871` | `0x00003` | u8[3]               | Unknown     | `unknown1` |
| `0x00874` | `0x00001` | u8                  | Y position  | `y`        |
| `0x00875` | `0x00003` | u8[3]               | Unknown     | `unknown2` |

## MinigameData

| Size      |
| --------- |
| `0x028f4` |

| Offset    | Size      | Type      | Description                       | JSON key      |
| --------- | --------- | --------- | --------------------------------- | ------------- |
| `0x00000` | `0x00004` | u32       | Checksum of the next 0x28f0 bytes | `checksum`    |
| `0x00004` | `0x028f0` | u8[10480] | ?                                 | `unknownData` |

## UnknownData

| Size      |
| --------- |
| `0x007f4` |

| Offset    | Size      | Type     | Description                      | JSON key      |
| --------- | --------- | -------- | -------------------------------- | ------------- |
| `0x00000` | `0x00004` | u32      | Checksum of the next 0x7f0 bytes | `checksum`    |
| `0x00004` | `0x007f0` | u8[2032] | ?                                | `unknownData` |
