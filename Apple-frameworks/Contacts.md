---
created: 2024-12-07 04:58:55
url: https://developer.apple.com/documentation/Contacts
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---

# Contacts
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---

Below is a comprehensive and organized set of Mermaid diagrams for the `Contacts` framework. These diagrams cover various aspects of the `Contacts` framework, including class structures, initializers, properties, methods, enumerations, protocol conformances, relationships with other classes, extensions, lifecycle, feature availability, data handling, integration, and best practices.

---

## **1. Class Structure and Hierarchy**

### **a. Core Class Diagram**
- **Purpose**: Illustrate the primary structure of the `Contacts` framework, including its key classes, properties, methods, and enumerations.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Classes**: `CNContact`, `CNContactStore`, `CNMutableContact`, `CNContactVCardSerialization`, etc.
  - **Properties**: Key attributes like `identifier`, `givenName`, `familyName`, etc.
  - **Methods**: Essential functions like `fetchContacts()`, `saveContact()`, etc.
  - **Enumerations**: Nested enums such as `CNContactSortOrder`, `CNContactStoreErrorCode`.

```mermaid
classDiagram
    class CNContact {
        +String identifier
        +String givenName
        +String familyName
        +String middleName
        +String nickname
        +String organizationName
        +String departmentName
        +String jobTitle
        +NSURL imageData
        +NSArray phoneNumbers
        +NSArray emailAddresses
        +NSArray postalAddresses
        +NSArray urlAddresses
        +NSArray socialProfiles
        +NSArray instantMessageAddresses
        +NSArray relatedNames
        +init()
        // Additional properties and methods...
    }

    class CNContactStore {
        +init()
        +NSArray unifiedContactsMatchingPredicate:error: Array<CNContact>
        +BOOL enumerateContactsWithFetchRequest:error: Array<CNContact>
        +BOOL save: CNContact
        +BOOL delete: CNContact
        // Additional properties and methods...
    }

    class CNMutableContact {
        +setGivenName(String)
        +setFamilyName(String)
        +setPhoneNumbers(Array<CNLabeledValue<CNPhoneNumber>>)
        +setEmailAddresses(Array<CNLabeledValue<NSString>>)
        +setPostalAddresses(Array<CNLabeledValue<CNPostalAddress>>)
        // Additional properties and methods...
    }

    class CNContactVCardSerialization {
        +Data dataWithContacts(Array<CNContact>)
        +Array<CNContact> contactsWithData(Data)
    }

    class CNContactSortOrder {
        <<enum>>
        +none
        +userDefault
        +givenName
        +familyName
    }

    class CNContactStoreErrorCode {
        <<enum>>
        +authorizationDenied
        +authorizationRestricted
        +calculation
        +vCardSerialization
        +unknown
    }

    CNContactStore --> CNContact
    CNMutableContact --> CNContact
    CNContactVCardSerialization --> CNContact
    CNContact --> CNContactSortOrder
    CNContactStore --> CNContactStoreErrorCode
```

---

## **2. Initializers Overview**

### **a. Initialization Methods Diagram**
- **Purpose**: Break down the various ways to instantiate contacts and related objects.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Contact Initialization**: `CNContact()`, `CNMutableContact()`
  - **Contact Store Initialization**: `CNContactStore()`
  - **Serialization Initialization**: `CNContactVCardSerialization()`
  - **Fetching Contacts**: `CNContactFetchRequest()`

```mermaid
graph LR
    A[Contacts Framework Initializers] --> B[Contact Initialization]
    A --> C[Contact Store Initialization]
    A --> D[Serialization Initialization]
    A --> E[Fetching Contacts]

    B --> B1["CNContact()"]
    B --> B2["CNMutableContact()"]

    C --> C1["CNContactStore()"]

    D --> D1["CNContactVCardSerialization()"]

    E --> E1["CNContactFetchRequest(keysToFetch: [CNKeyDescriptor])"]
    E --> E2["CNContactFetchRequest.predicate"]
```

---

## **3. Properties Breakdown**

### **a. Key Properties Diagram**
- **Purpose**: Detail the main properties of key classes within the `Contacts` framework.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **CNContact Properties**: `identifier`, `givenName`, `familyName`, `phoneNumbers`, `emailAddresses`, etc.
  - **CNContactStore Properties**: `defaultContainerIdentifier`, `groupsMatchingPredicate`
  - **CNMutableContact Properties**: Mutable versions of `CNContact` properties.

```mermaid
graph LR
    A[CNContact Properties] --> B[Basic Information]
    A --> C[Organization Details]
    A --> D[Contact Methods]
    A --> E[Addresses & URLs]
    A --> F[Social Profiles & Instant Messaging]

    B --> B1[identifier: String]
    B --> B2[givenName: String]
    B --> B3[familyName: String]
    B --> B4[middleName: String]
    B --> B5[nickname: String]

    C --> C1[organizationName: String]
    C --> C2[departmentName: String]
    C --> C3[jobTitle: String]

    D --> D1[phoneNumbers: Array<CNLabeledValue<CNPhoneNumber>>]
    D --> D2[emailAddresses: Array<CNLabeledValue<NSString>>]

    E --> E1[postalAddresses: Array<CNLabeledValue<CNPostalAddress>>]
    E --> E2[urlAddresses: Array<CNLabeledValue<NSString>>]

    F --> F1[socialProfiles: Array<CNLabeledValue<CNSocialProfile>>]
    F --> F2[instantMessageAddresses: Array<CNLabeledValue<CNInstantMessageAddress>>]
```

---

## **4. Methods Grouped by Functionality**

### **a. Contact Management Methods**
- **Purpose**: Categorize methods based on their roles in managing contacts.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Fetching Contacts**: `unifiedContactsMatchingPredicate:error:`, `enumerateContactsWithFetchRequest:error:`
  - **Saving Contacts**: `save:error:`, `delete:error:`
  - **Serialization**: `dataWithContacts:`, `contactsWithData:error:`
  - **Requesting Access**: `requestAccessForEntityType:completionHandler:`

```mermaid
flowchart TD
    A[CNContactStore Methods] --> B[Fetching Contacts]
    A --> C[Saving Contacts]
    A --> D[Serialization]
    A --> E[Requesting Access]

    B --> B1["unifiedContactsMatchingPredicate:error: -> Array<CNContact>"]
    B --> B2["enumerateContactsWithFetchRequest:error: -> BOOL"]

    C --> C1["save: CNContact -> BOOL"]
    C --> C2["delete: CNContact -> BOOL"]

    D --> D1["CNContactVCardSerialization.dataWithContacts(Array<CNContact>) -> Data"]
    D --> D2["CNContactVCardSerialization.contactsWithData(Data) -> Array<CNContact>"]

    E --> E1["requestAccessForEntityType:completionHandler: -> void"]
```

---

## **5. Enumerations and Configurations**

### **a. Enumerations Diagram**
- **Purpose**: Highlight the enums used within the `Contacts` framework and their possible values.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **CNContactSortOrder**
  - **CNContactStoreErrorCode**
  - **CNSocialProfileService**
  - **CNInstantMessageService**

```mermaid
classDiagram
    class CNContactSortOrder {
        <<enum>>
        +none
        +userDefault
        +givenName
        +familyName
    }

    class CNContactStoreErrorCode {
        <<enum>>
        +authorizationDenied
        +authorizationRestricted
        +calculation
        +vCardSerialization
        +unknown
    }

    class CNSocialProfileService {
        <<enum>>
        +facebook
        +twitter
        +linkedin
        +instagram
        +facebookMessager
        +weibo
    }

    class CNInstantMessageService {
        <<enum>>
        +facebook
        +twitter
        +googleTalk
        +jabber
        +icq
        +wechat
    }

    CNContactSortOrder <-- CNContactStoreErrorCode
    CNContactSortOrder <-- CNSocialProfileService
    CNContactSortOrder <-- CNInstantMessageService
```

### **b. Configuration Classes Diagram**
- **Purpose**: Show the relationship between core classes and their configuration or related classes.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **CNLabeledValue**
  - **CNPostalAddress**
  - **CNSocialProfile**
  - **CNInstantMessageAddress**

## TODO: Fix rendering syntax error

```mermaid
classDiagram
    class CNContact {
        +Array<CNLabeledValue<NSString>> emailAddresses
        +Array<CNLabeledValue<CNPhoneNumber>> phoneNumbers
        +Array<CNLabeledValue<CNPostalAddress>> postalAddresses
        +Array<CNLabeledValue<CNSocialProfile>> socialProfiles
        +Array<CNLabeledValue<CNInstantMessageAddress>> instantMessageAddresses
    }

    class CNLabeledValue<T> {
        +String label
        +T value
    }

    class CNPostalAddress {
        +String street
        +String city
        +String state
        +String postalCode
        +String country
        +String isoCountryCode
    }

    class CNSocialProfile {
        +NSString urlString
        +NSString username
        +NSString userIdentifier
        +CNSocialProfileService service
    }

    class CNInstantMessageAddress {
        +NSString username
        +CNInstantMessageService service
    }

    CNContact --> CNLabeledValue
    CNLabeledValue --> CNPostalAddress
    CNLabeledValue --> CNSocialProfile
    CNLabeledValue --> CNInstantMessageAddress
    
```

---

## **6. Protocol Conformances**

### **a. Protocols Diagram**
- **Purpose**: Display the protocols that key classes in the `Contacts` framework conform to and their impact.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **NSSecureCoding**
  - **NSCopying**
  - **CNKeyDescriptor**
  - **CNFetchRequest**

```mermaid
classDiagram
    class CNContact {
        <<class>>
    }

    class CNContactStore {
        <<class>>
    }

    class CNMutableContact {
        <<class>>
    }

    class CNKeyDescriptor {
        <<protocol>>
    }

    class CNFetchRequest {
        <<protocol>>
    }

    class NSSecureCoding {
        <<protocol>>
    }

    class NSCopying {
        <<protocol>>
    }

    CNContact ..|> NSSecureCoding
    CNContact ..|> NSCopying
    CNMutableContact ..|> CNContact
    CNContactStore ..|> CNFetchRequest
```

---

## **7. Relationships with Other Classes**

### **a. Related Classes Diagram**
- **Purpose**: Illustrate how the `Contacts` framework interacts with other Apple frameworks and classes.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **UIKit Integration**: `CNContactViewController`, `UIImage` for contact images.
  - **Foundation Framework**: `NSData`, `NSURL`, `NSDateComponents`.
  - **Core Data**: Integration for storing custom contact-related data.
  - **MapKit**: Displaying contact addresses on a map.
  - **UIKit.UIImage**: Handling contact images and thumbnails.

```mermaid
flowchart TD
    A[Contacts Framework] --> B[UIKit Integration]
    A --> C[Foundation Framework]
    A --> D[Core Data]
    A --> E[MapKit]
    A --> F[UIKit.UIImage]

    B --> B1[CNContactViewController]
    B --> B2[Displaying Contact Details]

    C --> C1[NSData]
    C --> C2[NSURL]
    C --> C3[NSDateComponents]

    D --> D1[Storing Custom Data]
    D --> D2[Fetching Custom Data]

    E --> E1[Displaying Addresses on Map]
    E --> E2[Geocoding Addresses]

    F --> F1[Handling Contact Images]
    F --> F2[Generating Thumbnails]
```

---

## **8. Extensions and Additional Functionalities**

### **a. Contacts Framework Extensions Diagram**
- **Purpose**: Showcase the additional functionalities provided through extensions.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **CNContact Extensions**
  - **CNContactStore Extensions**
  - **Helper Methods**
  - **Integration with Other Frameworks**

```mermaid
classDiagram
    class CNContact {
        <<class>>
    }

    class CNContactExtensions {
        <<extension>>
        +func fullName() -> String
        +func formattedAddress() -> String
        +func primaryEmail() -> String?
        +func primaryPhoneNumber() -> String?
        // Additional extended methods
    }

    class CNContactStoreExtensions {
        <<extension>>
        +func fetchContacts(withName name: String) -> [CNContact]
        +func fetchContacts(by email: String) -> [CNContact]
        +func fetchContacts(by phoneNumber: String) -> [CNContact]
        // Additional extended methods
    }

    CNContact <-- CNContactExtensions
    CNContactStore <-- CNContactStoreExtensions
```

### **b. Extensions Functionalities Flowchart**
- **Purpose**: Detail specific extended methods and their purposes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Helper Methods for Formatting**
  - **Advanced Fetching Techniques**
  - **Integration with UI Components**

```mermaid
flowchart LR
    A[Contacts Framework Extensions] --> B[Helper Methods]
    A --> C[Advanced Fetching]
    A --> D[UI Integration]

    B --> B1["fullName() -> String"]
    B --> B2["formattedAddress() -> String"]
    B --> B3["primaryEmail() -> String?"]
    B --> B4["primaryPhoneNumber() -> String?"]

    C --> C1["fetchContacts(withName: String) -> [CNContact]"]
    C --> C2["fetchContacts(byEmail: String) -> [CNContact]"]
    C --> C3["fetchContacts(byPhoneNumber: String) -> [CNContact]"]

    D --> D1["Displaying Contacts in UITableView"]
    D --> D2["Integrating with CNContactViewController"]
```

---

## **9. Lifecycle and Use Cases**

### **a. Lifecycle Flowchart**
- **Purpose**: Demonstrate the typical lifecycle of a `CNContact` within an application.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Initialization**
  - **Fetching**
  - **Modification**
  - **Saving**
  - **Deletion**
  - **Serialization**
  - **Displaying**

```mermaid
flowchart TD
    Start[Start] --> Init[Initialize CNContact or CNMutableContact]
    Init --> Fetch[Fetch Contacts from CNContactStore]
    Fetch --> Display[Display Contact in UI]
    Display --> Modify[Modify Contact Details]
    Modify --> Save[Save Changes to CNContactStore]
    Save --> Serialize[Serialize Contact Data]
    Serialize --> Cache[Cache or Share Data]
    Cache --> End[End]
```

### **b. Common Use Cases Diagram**
- **Purpose**: Outline the typical scenarios where the `Contacts` framework is utilized.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Displaying Contacts in UI**
  - **Editing Contact Information**
  - **Creating New Contacts**
  - **Deleting Contacts**
  - **Synchronizing Contacts with Server**
  - **Exporting Contacts as VCards**
  - **Integrating with Messaging or Email Apps**
  - **Displaying Contact Locations on Maps**

```mermaid
flowchart TD
    A[Contacts Framework Use Cases] --> B[Displaying Contacts in UI]
    A --> C[Editing Contact Information]
    A --> D[Creating New Contacts]
    A --> E[Deleting Contacts]
    A --> F[Synchronizing Contacts with Server]
    A --> G[Exporting Contacts as VCards]
    A --> H[Integrating with Messaging or Email Apps]
    A --> I[Displaying Contact Locations on Maps]
```

---

## **10. Feature Availability Timeline**

### **a. Feature Availability Gantt Chart**
- **Purpose**: Show when various `Contacts` framework features were introduced across iOS versions.
- **Diagram Type**: `gantt`
- **Contents**:
  - **iOS Versions**: 5.0, 6.0, 9.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0
  - **Features Introduced**: CNContactStore, CNContactVCardSerialization, CNContactViewController, Predicate-Based Fetching, Group Management, etc.

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title Contacts Framework Feature Availability

    section iOS 5.0
    CNContactStore & CNMutableContact          :done, des1, 2011-09-20, 2011-09-20

    section iOS 6.0
    CNContactVCardSerialization                :done, des2, 2012-09-17, 2012-09-17

    section iOS 9.0
    CNContactViewController                    :done, des3, 2015-09-16, 2015-09-16

    section iOS 10.0
    Predicate-Based Fetching                   :done, des4, 2016-09-13, 2016-09-13

    section iOS 11.0
    Group Management Support                   :done, des5, 2017-09-19, 2017-09-19

    section iOS 12.0
    Improved Privacy Controls                  :done, des6, 2018-09-17, 2018-09-17

    section iOS 13.0
    Unified Contacts Across Devices            :done, des7, 2019-09-19, 2019-09-19

    section iOS 14.0
    CNContactStore Extensions                  :done, des8, 2020-09-16, 2020-09-16

    section iOS 15.0
    Enhanced Serialization Options            :done, des9, 2021-09-20, 2021-09-20

    section iOS 16.0
    Advanced Fetching Capabilities             :done, des10, 2022-09-12, 2022-09-12

    section iOS 17.0
    Improved Integration with Other Frameworks :done, des11, 2023-09-18, 2023-09-18
```

---

## **11. Data Handling and Formats**

### **a. Contact Data Format Handling Diagram**
- **Purpose**: Explain how the `Contacts` framework handles different contact data formats.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **VCard Serialization**: `CNContactVCardSerialization`
  - **Data Encoding**: `NSData` handling for contacts
  - **JSON Integration**: Converting contacts to/from JSON if applicable

```mermaid
graph LR
    A[CNContact] --> B{Data Formats}
    B --> C[VCard Serialization]
    B --> D[JSON Integration]
    B --> E[Custom Data Encoding]

    C --> C1["CNContactVCardSerialization.dataWithContacts(Array<CNContact>) -> Data"]
    C --> C2["CNContactVCardSerialization.contactsWithData(Data) -> Array<CNContact>"]

    D --> D1["Custom Implementation for JSON Parsing"]
    E --> E1["NSData Encoding/Decoding"]
```

---

## **12. Integration with Other Contexts**

### **a. Integration Methods Diagram**
- **Purpose**: Show how the `Contacts` framework integrates with other application contexts and frameworks.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **UI Integration**: `CNContactViewController`, `UITableView`
  - **Networking**: Syncing contacts with remote servers
  - **Persistence**: Saving custom contact-related data with Core Data
  - **Mapping**: Displaying contact addresses using `MapKit`
  - **Third-Party Services**: Integrating with messaging or email services

```mermaid
flowchart TD
    A[Contacts Framework Integration] --> B[UI Integration]
    A --> C[Networking]
    A --> D[Persistence]
    A --> E[Mapping]
    A --> F[Third-Party Services]

    B --> B1[CNContactViewController]
    B --> B2[Displaying in UITableView]

    C --> C1[Syncing with Remote Servers]
    C --> C2[API Communication]

    D --> D1[Core Data Integration]
    D --> D2[Storing Additional Data]

    E --> E1[Displaying Addresses on MapKit]
    E --> E2[Geocoding Addresses]

    F --> F1[Messaging Services Integration]
    F --> F2[Email Services Integration]
```

---

## **13. Summary and Best Practices**

### **a. Summary Diagram**
- **Purpose**: Provide a high-level overview of the `Contacts` framework's key characteristics and functionalities.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Comprehensive Contact Management**
  - **Robust Data Handling**
  - **Seamless UI Integration**
  - **Advanced Fetching and Searching**
  - **Privacy and Security**
  - **Extensibility and Customization**
  - **Integration with Other Frameworks**

```mermaid
graph LR
    A[Contacts Framework] --> B[Comprehensive Contact Management]
    A --> C[Robust Data Handling]
    A --> D[Seamless UI Integration]
    A --> E[Advanced Fetching and Searching]
    A --> F[Privacy and Security]
    A --> G[Extensibility and Customization]
    A --> H[Integration with Other Frameworks]

    B --> B1[Create, Read, Update, Delete Contacts]
    C --> C1[VCard Serialization]
    C --> C2[Data Encoding]
    D --> D1[CNContactViewController Integration]
    D --> D2[Displaying in Tables and Lists]
    E --> E1[Predicate-Based Fetching]
    E --> E2[Efficient Searching]
    F --> F1[Access Permissions]
    F --> F2[Data Protection]
    G --> G1[Extensions and Helper Methods]
    G --> G2[Custom Data Integration]
    H --> H1[MapKit for Address Display]
    H --> H2[Core Data for Persistence]
```

### **b. Best Practices Diagram**
- **Purpose**: Outline best practices when using the `Contacts` framework.
- **Diagram Type**: `mindmap`
- **Contents**:
  - **Efficient Data Fetching**
  - **Respecting User Privacy**
  - **Handling Permissions Gracefully**
  - **Optimizing Performance**
  - **Ensuring Data Consistency**
  - **Error Handling and Recovery**
  - **User-Friendly UI Integration**
  - **Leveraging Extensions for Customization**

## TODO: Fix rendering syntax error

```mermaid
mindmap
  root((Best Practices))

  root --> EfficientDataFetching((Efficient Data Fetching))
  root --> RespectingUserPrivacy((Respecting User Privacy))
  root --> HandlingPermissionsGracefully((Handling Permissions Gracefully))
  root --> OptimizingPerformance((Optimizing Performance))
  root --> EnsuringDataConsistency((Ensuring Data Consistency))
  root --> ErrorHandlingRecovery((Error Handling and Recovery))
  root --> UserFriendlyUIIntegration((User-Friendly UI Integration))
  root --> LeveragingExtensions((Leveraging Extensions for Customization))

  EfficientDataFetching --> OptimizeFetchRequests((Optimize Fetch Requests))
  EfficientDataFetching --> UsePredicates((Use Predicates Effectively))

  RespectingUserPrivacy --> RequestOnlyNeededData((Request Only Needed Data))
  RespectingUserPrivacy --> InformUsers((Inform Users About Data Usage))

  HandlingPermissionsGracefully --> CheckAuthorizationStatus((Check Authorization Status))
  HandlingPermissionsGracefully --> ProvideFallbacks((Provide Fallbacks if Access Denied))

  OptimizingPerformance --> CacheFrequentlyUsedData((Cache Frequently Used Data))
  OptimizingPerformance --> PerformHeavyTasksAsync((Perform Heavy Tasks Asynchronously))

  EnsuringDataConsistency --> ValidateDataBeforeSaving((Validate Data Before Saving))
  EnsuringDataConsistency --> HandleConflicts((Handle Data Conflicts))

  ErrorHandlingRecovery --> ImplementRobustErrorHandling((Implement Robust Error Handling))
  ErrorHandlingRecovery --> ProvideUserFeedback((Provide Meaningful User Feedback))

  UserFriendlyUIIntegration --> UseStandard UI Components((Use Standard UI Components))
  UserFriendlyUIIntegration --> CustomizeWhenNecessary((Customize When Necessary))

  LeveragingExtensions --> CreateHelperMethods((Create Helper Methods))
  LeveragingExtensions --> Extend Functionality((Extend Functionality as Needed))
  
```

---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---