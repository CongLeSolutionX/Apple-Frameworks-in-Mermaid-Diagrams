---
created: 2024-12-07 04:58:55
url:
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
---


# PhotoTypes in PhotoKit framework
 
Below is a set of Mermaid diagrams to visually represent the relationships and structures of the enums and structs within the `PhotoKit` framework. These diagrams should help developers better understand the concepts and serve as a future reference.

---

## 1. Overview of Photos Framework Enums and Structures

```mermaid
graph TD
    PhotosFramework[Photos Framework API] --> Enums
    PhotosFramework --> Structures
    PhotosFramework --> Extensions

    Enums --> PHImageContentMode
    Enums --> PHCollectionListType
    Enums --> PHCollectionListSubtype
    Enums --> PHCollectionEditOperation
    Enums --> PHAssetCollectionType
    Enums --> PHAssetCollectionSubtype
    Enums --> PHAssetEditOperation
    Enums --> PHAssetMediaType
    Enums --> PHObjectType
    Structures --> PHAssetMediaSubtype
    Structures --> PHAssetBurstSelectionType
    Structures --> PHAssetSourceType
    Structures --> PHAssetResourceType
    Extensions --> PHAssetPlaybackStyle
```

---

## 2. PHImageContentMode Enum

```mermaid
classDiagram
    class PHImageContentMode {
        <<enumeration>>
        +aspectFit = 0
        +aspectFill = 1
        +default: PHImageContentMode
    }
```

**Description:**
Defines how an image should be resized or scaled within a given space.

---

## 3. PHCollectionListType Enum

```mermaid
classDiagram
    class PHCollectionListType {
        <<enumeration>>
        +momentList = 1
        +folder = 2
        +smartFolder = 3
    }

    PHCollectionListType : +momentList is deprecated in iOS 13
```

**Description:**
Specifies the type of a collection list, such as moments, folders, or smart folders.

---

## 4. PHCollectionListSubtype Enum

```mermaid
classDiagram
    class PHCollectionListSubtype {
        <<enumeration>>
        +momentListCluster = 1
        +momentListYear = 2
        +regularFolder = 100
        +smartFolderEvents = 200
        +smartFolderFaces = 201
        +any = 9223372036854775807
        
        % Deprecated Cases
        +momentListCluster~deprecated in iOS 13~
        +momentListYear~deprecated in iOS 13~
    }
```

**Description:**
Further categorizes collection lists with specific subtypes, including deprecated moment list types and various folder types.


## PHCollectionListType and PHCollectionListSubtype Enumerations

```mermaid
classDiagram
    class PHCollectionListType {
        <<Enumeration>>
        + momentList~deprecated~
        + folder
        + smartFolder
    }

    class PHCollectionListSubtype {
        <<Enumeration>>
        + momentListCluster~deprecated~
        + momentListYear~deprecated~
        + regularFolder
        + smartFolderEvents
        + smartFolderFaces
        + any
    }

    PHCollectionListType --> PHCollectionListSubtype : specifies
```

---

## 5. PHCollectionEditOperation Enum

```mermaid
classDiagram
    class PHCollectionEditOperation {
        <<enumeration>>
        +deleteContent = 1
        +removeContent = 2
        +addContent = 3
        +createContent = 4
        +rearrangeContent = 5
        +delete = 6
        +rename = 7
    }
```

**Description:**
Enumerates the possible edit operations that can be performed on a photo collection.

---

## 6. PHAssetCollectionType Enum

```
classDiagram
    class PHAssetCollectionType {
        <<enumeration>>
        +album = 1
        +smartAlbum = 2
        +moment = 3
    }

    PHAssetCollectionType : +moment is deprecated in iOS 13
}
```

**Description:**
Defines the type of an asset collection, such as albums, smart albums, or moments (deprecated).

---

## 7. PHAssetCollectionSubtype Enum

```mermaid
classDiagram
    class PHAssetCollectionSubtype {
        <<enumeration>>
        +albumRegular = 2
        +albumSyncedEvent = 3
        +albumSyncedFaces = 4
        +albumSyncedAlbum = 5
        +albumImported = 6
        +albumMyPhotoStream = 100
        +albumCloudShared = 101
        +smartAlbumGeneric = 200
        +smartAlbumPanoramas = 201
        +smartAlbumVideos = 202
        +smartAlbumFavorites = 203
        +smartAlbumTimelapses = 204
        +smartAlbumAllHidden = 205
        +smartAlbumRecentlyAdded = 206
        +smartAlbumBursts = 207
        +smartAlbumSlomoVideos = 208
        +smartAlbumUserLibrary = 209
        +smartAlbumSelfPortraits = 210
        +smartAlbumScreenshots = 211
        +smartAlbumDepthEffect = 212
        +smartAlbumLivePhotos = 213
        +smartAlbumAnimated = 214
        +smartAlbumLongExposures = 215
        +smartAlbumUnableToUpload = 216
        +smartAlbumRAW = 217
        +smartAlbumCinematic = 218
        +smartAlbumSpatial = 219
        +any = 9223372036854775807
    }
```

**Description:**
Provides detailed subtypes for asset collections, including various album types and smart album categories, with support for modern features like Live Photos and Cinematic.


## PHAssetCollectionType and PHAssetCollectionSubtype Enumerations

```mermaid
classDiagram
    class PHAssetCollectionType {
        <<Enumeration>>
        + album
        + smartAlbum
        + moment~deprecated~
    }

    class PHAssetCollectionSubtype {
        <<Enumeration>>
        // Albums
        + albumRegular
        + albumSyncedEvent
        + albumSyncedFaces
        + albumSyncedAlbum
        + albumImported
        + albumMyPhotoStream
        + albumCloudShared

        // Smart Albums
        + smartAlbumGeneric
        + smartAlbumPanoramas
        + smartAlbumVideos
        + smartAlbumFavorites
        + smartAlbumTimelapses
        + smartAlbumAllHidden
        + smartAlbumRecentlyAdded
        + smartAlbumBursts
        + smartAlbumSlomoVideos
        + smartAlbumUserLibrary
        + smartAlbumSelfPortraits
        + smartAlbumScreenshots
        + smartAlbumDepthEffect
        + smartAlbumLivePhotos
        + smartAlbumAnimated
        + smartAlbumLongExposures
        + smartAlbumUnableToUpload
        + smartAlbumRAW
        + smartAlbumCinematic
        + smartAlbumSpatial
        + any
    }

    PHAssetCollectionType --> PHAssetCollectionSubtype : further specifies
```


**Description:**

- **PHAssetCollectionType** defines the types of asset collections (e.g., album, smart album).
- **PHAssetCollectionSubtype** provides detailed subtypes, categorized into Albums and Smart Albums.
- Deprecated items are marked with `~deprecated~`.


---

## 8. PHAssetEditOperation Enum

```mermaid
classDiagram
    class PHAssetEditOperation {
        <<enumeration>>
        +delete = 1
        +content = 2
        +properties = 3
    }
```

**Description:**
Enumerates the types of edit operations applicable to individual assets.

---

## 9. PHAssetMediaType Enum

```mermaid
classDiagram
    class PHAssetMediaType {
        <<enumeration>>
        +unknown = 0
        +image = 1
        +video = 2
        +audio = 3
    }
```

**Description:**
Defines the media type of an asset, such as image, video, or audio.

---

## 10. PHObjectType Enum

```mermaid
classDiagram
    class PHObjectType {
        <<enumeration>>
        +asset = 1
        +assetCollection = 2
        +collectionList = 3
    }
```

**Description:**
Specifies the type of a `PHObject`, indicating whether it’s an asset, asset collection, or collection list.

---

## 11. PHAssetMediaSubtype OptionSet

```mermaid
classDiagram
    class PHAssetMediaSubtype {
        <<OptionSet>>
        +photoPanorama
        +photoHDR
        +photoScreenshot
        +photoLive
        +photoDepthEffect
        +spatialMedia
        +videoStreamed
        +videoHighFrameRate
        +videoTimelapse
        +videoCinematic
    }
```

Another diagram representation: 

```mermaid
flowchart TD
    Start[Start] --> A[PHAssetMediaSubtype]
    A --> B{Is Photo?}
    B --> |Yes| C[Check Photo Subtypes]
    B --> |No| D[Check Video Subtypes]
    C --> E[photoPanorama]
    C --> F[photoHDR]
    C --> G[photoScreenshot]
    C --> H[photoLive]
    C --> I[photoDepthEffect]
    C --> J[spatialMedia]
    D --> K[videoStreamed]
    D --> L[videoHighFrameRate]
    D --> M[videoTimelapse]
    D --> N[videoCinematic]
```



**Description:**
Represents advanced media subtypes for assets, allowing combination of multiple attributes such as HDR, Panoramas, Live Photos, and various video enhancements.

---

## 12. PHAssetBurstSelectionType OptionSet

```mermaid
classDiagram
    class PHAssetBurstSelectionType {
        <<OptionSet>>
        +autoPick
        +userPick
    }
```

**Description:**
Indicates the selection type for burst photos, distinguishing between automatic and user-selected picks.

---

## 13. PHAssetSourceType OptionSet

```mermaid
classDiagram
    class PHAssetSourceType {
        <<OptionSet>>
        +typeUserLibrary
        +typeCloudShared
        +typeiTunesSynced
    }
```

**Description:**
Specifies the source of an asset, such as the user’s library, cloud-shared albums, or iTunes-synced content.

---

## 14. PHAssetResourceType Enum


```mermaid
flowchart TD
    A[PHAssetResourceType]
    A --> |1| B[photo]
    A --> |2| C[video]
    A --> |3| D[audio]
    A --> |4| E[alternatePhoto]
    A --> |5| F[fullSizePhoto]
    A --> |6| G[fullSizeVideo]
    A --> |7| H[adjustmentData]
    A --> |8| I[adjustmentBasePhoto]
    A --> |9| J[pairedVideo]
    A --> |10| K[fullSizePairedVideo]
    A --> |11| L[adjustmentBasePairedVideo]
    A --> |12| M[adjustmentBaseVideo]
    A --> |19| N[photoProxy]
```


**Description:**

- Enumerates all possible resource types associated with a PHAsset.
- Each node represents a resource type with its corresponding enum value.
- photoProxy is available in iOS 17

---

## TODO: Fix diagram syntax error

## 15. PHAsset Extension: PlaybackStyle Enum

```
classDiagram
    class PHAsset.PlaybackStyle {
        <<enumeration>>
        +unsupported = 0
        +image = 1
        +imageAnimated = 2
        +livePhoto = 3
        +video = 4
        +videoLooping = 5
    }
```

**Description:**
Defines how an asset should be played back, distinguishing between static images, animated images, Live Photos, and various video styles.

---

## 16. Relationships and Dependencies

```mermaid
graph TD
    PHAsset --> PHAssetMediaType
    PHAsset --> PHAssetMediaSubtype
    PHAsset --> PHAssetBurstSelectionType
    PHAsset --> PHAssetSourceType
    PHAsset --> PHAssetResourceType
    PHAsset --> PlaybackStyle
    PHAssetCollection --> PHAssetCollectionType
    PHAssetCollection --> PHAssetCollectionSubtype
    PHCollectionList --> PHCollectionListType
    PHCollectionList --> PHCollectionListSubtype

    PHAssetEditOperation --> PHAssetCollection
    PHCollectionEditOperation --> PHCollectionList
    PHObjectType --> PHAsset
    PHObjectType --> PHAssetCollection
    PHObjectType --> PHCollectionList
```

**Description:**
Illustrates the relationships and dependencies between different enums and structures within the `Photos` framework, highlighting how assets, collections, and their respective types and subtypes interrelate.

---

## 17. Deprecated Elements


```mermaid
graph TD
    A[Enumerations] --> B[Version Availability]
    B --> C[Introduced in iOS 8]
    B --> D[Deprecated Items]
    D --> E[PHCollectionListType.momentList]
    D --> F[PHCollectionListSubtype.momentListCluster]
    D --> G[PHCollectionListSubtype.momentListYear]
    D --> H[PHAssetCollectionType.moment]
```

Another way to represent this section: 

```mermaid
classDiagram
    class PHCollectionListType {
        <<enumeration>>
        +momentList = 1 (Deprecated in iOS 13)
    }

    class PHCollectionListSubtype {
        <<enumeration>>
        +momentListCluster = 1 (Deprecated in iOS 13)
        +momentListYear = 2 (Deprecated in iOS 13)
    }

    class PHAssetCollectionType {
        <<enumeration>>
        +moment = 3 (Deprecated in iOS 13)
    }
```

**Description:**
- Highlights the importance of checking the availability and deprecation status.
- Developers should be aware of deprecated items to maintain forward compatibility.


---
