---
created: 2024-12-07 04:58:55
url:
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
---

# UITableViewController


Below is a comprehensive and organized set of Mermaid diagrams for the `UITableViewController` class. These diagrams will cover various aspects of `UITableViewController`, including its class hierarchy, initialization methods, properties, methods, protocol conformances, relationships with other classes, extensions, lifecycle, use cases, feature availability, data handling, integrations, and best practices.

---

## **1. Class Structure and Hierarchy**

### **a. Core Class Diagram**
- **Purpose**: Illustrate the primary structure of `UITableViewController`, including its properties, methods, and relevant inherited classes.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Properties**: Key attributes like `tableView`, `clearsSelectionOnViewWillAppear`, etc.
  - **Methods**: Essential functions like initializers, lifecycle methods (`viewDidLoad()`, `viewWillAppear(_:)`, etc.), and table view management methods.
  - **Inheritance**: Shows that `UITableViewController` inherits from `UIViewController` and conforms to `UITableViewDelegate` and `UITableViewDataSource`.

```mermaid
classDiagram
    class UITableViewController {
        +tableView: UITableView
        +clearsSelectionOnViewWillAppear: Bool
        +refreshControl: UIRefreshControl?
        +init(style: UITableView.Style)
        +init?(coder: NSCoder)
        +viewDidLoad()
        +viewWillAppear(_ animated: Bool)
        +numberOfSections(in tableView: UITableView) -> Int
        +tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int
        +tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell
        +tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath)
        // Additional properties and methods...
    }

    class UIViewController {
        <<open class>>
    }

    class UITableViewDelegate {
        <<protocol>>
    }

    class UITableViewDataSource {
        <<protocol>>
    }

    UITableViewController --|> UIViewController
    UITableViewController ..|> UITableViewDelegate
    UITableViewController ..|> UITableViewDataSource
```

---

## **2. Initializers Overview**

### **a. Initialization Methods Diagram**
- **Purpose**: Break down the various ways to instantiate `UITableViewController`.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Designated Initializers**: `init(style:)`
  - **Convenience Initializers**: `init(coder:)`
  - **Storyboard Integration**: Initializing via Storyboards and Nibs

```mermaid
graph LR
    A[UITableViewController Initializers] --> B[Designated Initializers]
    A --> C[Convenience Initializers]
    A --> D[Storyboard Integration]

    B --> B1["init(style: UITableView.Style)"]
    
    C --> C1["init?(coder: NSCoder)"]
    
    D --> D1["Initialize via Storyboard"]
    D --> D2["Initialize via Nib"]
```

---

## **3. Properties Breakdown**

### **a. Key Properties Diagram**
- **Purpose**: Detail the main properties of `UITableViewController`.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Table View Management**: `tableView`
  - **Selection Handling**: `clearsSelectionOnViewWillAppear`
  - **Refresh Control**: `refreshControl`
  - **Editing Mode**: `isEditing`
  - **Style**: `style`
  - **Additional Properties**: `definesPresentationContext`, `extendedLayoutIncludesOpaqueBars`, etc.

```mermaid
graph LR
    A[UITableViewController Properties] --> B[Table View Management]
    A --> C[Selection Handling]
    A --> D[Refresh Control]
    A --> E[Editing Mode]
    A --> F[Style]
    A --> G[Additional Properties]

    B --> B1[tableView: UITableView]
    
    C --> C1[clearsSelectionOnViewWillAppear: Bool]
    
    D --> D1[refreshControl: UIRefreshControl?]
    
    E --> E1[isEditing: Bool]
    
    F --> F1[style: UITableView.Style]
    
    G --> G1[definesPresentationContext: Bool]
    G --> G2[extendedLayoutIncludesOpaqueBars: Bool]
    G --> G3[additional setups...]
```

---

## **4. Methods Grouped by Functionality**

### **a. Lifecycle Methods**
- **Purpose**: Categorize lifecycle-related methods of `UITableViewController`.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **View Loading**: `viewDidLoad()`, `viewWillAppear(_:)`, `viewDidAppear(_:)`, etc.
  - **View Unloading**: `viewWillDisappear(_:)`, `viewDidDisappear(_:)`
  - **Memory Management**: `didReceiveMemoryWarning()`

```mermaid
flowchart TD
    A[Lifecycle Methods] --> B[View Loading]
    A --> C[View Unloading]
    A --> D[Memory Management]

    B --> B1["viewDidLoad()"]
    B --> B2["viewWillAppear(_ animated: Bool)"]
    B --> B3["viewDidAppear(_ animated: Bool)"]

    C --> C1["viewWillDisappear(_ animated: Bool)"]
    C --> C2["viewDidDisappear(_ animated: Bool)"]

    D --> D1["didReceiveMemoryWarning()"]
```

### **b. Table View Data Source Methods**
- **Purpose**: Group methods responsible for providing data to the table view.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Section Management**: `numberOfSections(in:)`
  - **Row Management**: `tableView(_:numberOfRowsInSection:)`, `tableView(_:cellForRowAt:)`
  - **Dynamic Row Heights**: `tableView(_:heightForRowAt:)`
  - **Editing Procedures**: `tableView(_:canEditRowAt:)`, `tableView(_:commit:forRowAt:)`

```mermaid
flowchart TD
    A[Table View Data Source Methods] --> B[Section Management]
    A --> C[Row Management]
    A --> D[Dynamic Row Heights]
    A --> E[Editing Procedures]

    B --> B1["numberOfSections(in tableView: UITableView) -> Int"]

    C --> C1["tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int"]
    C --> C2["tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell"]

    D --> D1["tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat"]

    E --> E1["tableView(_ tableView: UITableView, canEditRowAt indexPath: IndexPath) -> Bool"]
    E --> E2["tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath)"]
```

### **c. Table View Delegate Methods**
- **Purpose**: Group methods that handle user interactions and table view behavior.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Row Selection**: `tableView(_:didSelectRowAt:)`, `tableView(_:didDeselectRowAt:)`
  - **Row Actions**: `tableView(_:editActionsForRowAt:)`
  - **Header and Footer Management**: `tableView(_:viewForHeaderInSection:)`, `tableView(_:heightForHeaderInSection:)`, etc.
  - **Accessory Type Handling**: `tableView(_:accessoryButtonTappedForRowWith:)`

```mermaid
flowchart TD
    A[Table View Delegate Methods] --> B[Row Selection]
    A --> C[Row Actions]
    A --> D[Header and Footer Management]
    A --> E[Accessory Type Handling]

    B --> B1["tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath)"]
    B --> B2["tableView(_ tableView: UITableView, didDeselectRowAt indexPath: IndexPath)"]

    C --> C1["tableView(_ tableView: UITableView, editActionsForRowAt indexPath: IndexPath) -> [UITableViewRowAction]?"]

    D --> D1["tableView(_ tableView: UITableView, viewForHeaderInSection section: Int) -> UIView?"]
    D --> D2["tableView(_ tableView: UITableView, heightForHeaderInSection section: Int) -> CGFloat"]
    D --> D3["tableView(_ tableView: UITableView, viewForFooterInSection section: Int) -> UIView?"]
    D --> D4["tableView(_ tableView: UITableView, heightForFooterInSection section: Int) -> CGFloat"]

    E --> E1["tableView(_ tableView: UITableView, accessoryButtonTappedForRowWith indexPath: IndexPath)"]
```

### **d. Editing and Reordering Methods**
- **Purpose**: Categorize methods related to editing and reordering table view cells.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Commit Editing Style**: `tableView(_:commit:forRowAt:)`
  - **Move Row**: `tableView(_:moveRowAt:to:)`
  - **Can Move Row**: `tableView(_:canMoveRowAt:)`

```mermaid
flowchart TD
    A[Editing and Reordering Methods] --> B[Commit Editing Style]
    A --> C[Move Row]
    A --> D[Can Move Row]

    B --> B1["tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath)"]

    C --> C1["tableView(_ tableView: UITableView, moveRowAt sourceIndexPath: IndexPath, to destinationIndexPath: IndexPath)"]

    D --> D1["tableView(_ tableView: UITableView, canMoveRowAt indexPath: IndexPath) -> Bool"]
```

---

## **5. Enumerations and Configurations**

### **a. Enumerations Diagram**
- **Purpose**: Highlight the enums used within `UITableViewController` and related to its configurations.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Table View Styles**: `UITableView.Style`
  - **Editing Styles**: `UITableViewCell.EditingStyle`
  - **Row Actions**: `UITableView.RowAction`
  - **Section Types**: `UITableView.Section`

## TODO: Fix diagram syntax error 

```mermaid
classDiagram
    class UITableViewController {
        <<enumeration>> Style
        <<enumeration>> EditingStyle
        <<enumeration>> RowAction
        <<enumeration>> Section
    }

    class UITableView.Style {
        +plain
        +grouped
        +insetGrouped
        +sidebar
    }

    class UITableViewCell.EditingStyle {
        +none
        +delete
        +insert
    }

    class UITableView.RowAction {
        +style
        +title
        +handler
    }

    class UITableView.Section {
        +header
        +footer
        +rows
    }

    UITableViewController --> UITableView.Style
    UITableViewController --> UITableViewCell.EditingStyle
    UITableViewController --> UITableView.RowAction
    UITableViewController --> UITableView.Section
    
```

### **b. Configuration Classes Diagram**
- **Purpose**: Show the relationship between `UITableViewController` and its configuration classes.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **UITableView**: Managed table view instance
  - **UIRefreshControl**: For pull-to-refresh functionality

```mermaid
classDiagram
    class UITableViewController {
        +tableView: UITableView
        +refreshControl: UIRefreshControl?
    }

    class UITableView {
        +delegate: UITableViewDelegate?
        +dataSource: UITableViewDataSource?
        +register(_ nib: UINib?, forCellReuseIdentifier identifier: String)
        +dequeueReusableCell(withIdentifier identifier: String, for indexPath: IndexPath) -> UITableViewCell
        +reloadData()
        // Additional properties and methods...
    }

    class UIRefreshControl {
        +beginRefreshing()
        +endRefreshing()
        +addTarget(_ target: Any?, action: Selector, for controlEvents: UIControl.Event)
        // Additional properties and methods...
    }

    UITableViewController --> UITableView
    UITableViewController --> UIRefreshControl
```

---

## **6. Protocol Conformances**

### **a. Protocols Diagram**
- **Purpose**: Display the protocols that `UITableViewController` conforms to and their impact.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **UITableViewDelegate**
  - **UITableViewDataSource**
  - **UISearchResultsUpdating** (if applicable)
  - **UIContextMenuInteractionDelegate** (for context menus)

```mermaid
classDiagram
    class UITableViewController {
        <<open class>>
    }

    class UITableViewDelegate {
        <<protocol>>
    }

    class UITableViewDataSource {
        <<protocol>>
    }

    class UISearchResultsUpdating {
        <<protocol>>
    }

    class UIContextMenuInteractionDelegate {
        <<protocol>>
    }

    UITableViewController ..|> UITableViewDelegate
    UITableViewController ..|> UITableViewDataSource
    UITableViewController ..|> UISearchResultsUpdating
    UITableViewController ..|> UIContextMenuInteractionDelegate
```

---

## **7. Relationships with Other Classes**

### **a. Related Classes Diagram**
- **Purpose**: Illustrate how `UITableViewController` interacts with other UIKit classes and frameworks.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **UITableView**: Primary table view managed by the controller.
  - **UITableViewCell**: Cells displayed within the table view.
  - **UIViewController**: Parent class providing view lifecycle.
  - **UISearchController**: For adding search capabilities.
  - **UIRefreshControl**: For pull-to-refresh functionality.
  - **Navigation Controllers**: For managing navigation stacks.
  - **Storyboard & Nib Files**: For UI design and instantiation.

```mermaid
flowchart TD
    A[UITableViewController] --> B[UITableView]
    A --> C[UITableViewCell]
    A --> D[UIViewController]
    A --> E[UISearchController]
    A --> F[UIRefreshControl]
    A --> G[UINavigationController]
    A --> H[Storyboard & Nib Files]

    B --> |manages| C
    A --> |inherits from| D
    A --> |integrates with| E
    A --> |uses| F
    A --> |embedded in| G
    A --> |instantiated via| H
```

---

## **8. Extensions and Additional Functionalities**

### **a. UITableViewController Extensions Diagram**
- **Purpose**: Showcase the additional functionalities provided through extensions.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Data Handling Extensions**: Methods for handling data sources and delegates.
  - **UI Enhancements**: Methods for customizing table view appearance and behavior.
  - **Convenience Methods**: Helper functions for common tasks.

```mermaid
classDiagram
    class UITableViewController {
        <<open class>>
    }

    class UITableViewControllerExtensions {
        <<extension>>
        +func configureTableViewAppearance()
        +func setupRefreshControl()
        +func registerCells()
        +func handleRowSelection(indexPath: IndexPath)
        // Additional extended methods
    }

    UITableViewController <-- UITableViewControllerExtensions
```

### **b. Extensions Functionalities Flowchart**
- **Purpose**: Detail specific extended methods and their purposes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Table View Configuration**
  - **Data Binding**
  - **UI Customization**

```mermaid
flowchart LR
    A[UITableViewController Extensions] --> B[Table View Configuration]
    A --> C[Data Binding]
    A --> D[UI Customization]

    B --> B1["configureTableViewAppearance()"]
    B --> B2["registerCells()"]

    C --> C1["bindDataToTableView(data: [DataModel])"]
    C --> C2["updateTableView()"]

    D --> D1["customizeRowAppearance()"]
    D --> D2["setupRefreshControl()"]
```

---

## **9. Lifecycle and Use Cases**

### **a. Lifecycle Flowchart**
- **Purpose**: Demonstrate the typical lifecycle of a `UITableViewController` within an application.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Initialization**
  - **View Loading**
  - **Displaying Data**
  - **User Interaction**
  - **Data Refreshing**
  - **View Unloading**
  - **Deinitialization**

```mermaid
flowchart TD
    Start[Start] --> Init[Initialize UITableViewController]
    Init --> LoadView[Load View and TableView]
    LoadView --> DisplayData[Display Data in TableView]
    DisplayData --> UserInteraction[Handle User Interactions]
    UserInteraction --> Refresh[Pull to Refresh or Update Data]
    Refresh --> DisplayData
    UserInteraction --> Navigate[Navigate to Other Screens]
    Navigate --> End[End]
    Refresh --> End
    DisplayData --> Unload[Unload View]
    Unload --> Deinit[Deinitialize UITableViewController]
    Deinit --> End
```

### **b. Common Use Cases Diagram**
- **Purpose**: Outline the typical scenarios where `UITableViewController` is utilized.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Displaying Lists**: Static and dynamic lists.
  - **Form Inputs**: Creating forms with multiple input fields.
  - **Settings Screens**: Managing app settings.
  - **Data-Driven Interfaces**: Displaying data from APIs or local databases.
  - **Interactive Tables**: Drag-and-drop reordering, swipe actions.
  - **Nested Tables**: Master-detail interfaces.

```mermaid
flowchart TD
    A[UITableViewController Use Cases] --> B[Displaying Lists]
    A --> C[Form Inputs]
    A --> D[Settings Screens]
    A --> E[Data-Driven Interfaces]
    A --> F[Interactive Tables]
    A --> G[Nested Tables]

    B --> B1[Static Lists]
    B --> B2[Dynamic Lists with Data]
    
    C --> C1[Multiple Input Fields]
    C --> C2[Validation and Submission]
    
    D --> D1[App Settings Management]
    D --> D2[User Preferences]
    
    E --> E1[Fetching Data from APIs]
    E --> E2[Local Database Integration]
    
    F --> F1[Drag-and-Drop Reordering]
    F --> F2[Swipe Actions for Cells]
    
    G --> G1[Master-Detail Interfaces]
    G --> G2[Nested TableViews]
```

---

## **10. Feature Availability Timeline**

### **a. Feature Availability Gantt Chart**
- **Purpose**: Show when various `UITableViewController` features were introduced across iOS versions.
- **Diagram Type**: `gantt`
- **Contents**:
  - **iOS Versions**: 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0
  - **Features Introduced**: Pull-to-Refresh, Self-Sizing Cells, Swipe Actions, Context Menus, Diffable Data Sources, UIRefreshControl enhancements, etc.

## TODO: Fix diagram syntax error

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title UITableViewController Feature Availability

    section iOS 3.0
    Basic UITableViewController            :done, des1, 2009-06-17, 2009-06-17

    section iOS 4.0
    Pull to Refresh                        :done, des2, 2010-06-21, 2010-06-21

    section iOS 5.0
    Self-Sizing Cells                      :done, des3, 2011-10-12, 2011-10-12

    section iOS 6.0
    Section Index Titles                   :done, des4, 2012-09-19, 2012-09-19

    section iOS 7.0
    Interactive Rows                       :done, des5, 2013-09-18, 2013-09-18

    section iOS 8.0
    Swipe Actions                          :done, des6, 2014-09-17, 2014-09-17

    section iOS 9.0
    Context Menus                          :done, des7, 2015-09-16, 2015-09-16

    section iOS 10.0
    Refresh Control Enhancements           :done, des8, 2016-09-19, 2016-09-19

    section iOS 11.0
    Drag and Drop                          :done, des9, 2017-09-19, 2017-09-19

    section iOS 12.0
    Multi-Section Headers & Footers        :done, des10, 2018-09-17, 2018-09-17

    section iOS 13.0
    Diffable Data Sources                  :done, des11, 2019-09-19, 2019-09-19

    section iOS 14.0
    Swipe Gestures Customization           :done, des12, 2020-09-16, 2020-09-16

    section iOS 15.0
    Improved Performance and Memory Usage  :done, des13, 2021-09-20, 2021-09-20

    section iOS 16.0
    Custom Swipe Actions with UIContextualAction :done, des14, 2022-09-12, 2022-09-12

    section iOS 17.0
    Enhanced Context Menus and Drag-and-Drop Support :done, des15, 2023-09-18, 2023-09-18
```

---

## **11. Data Handling and Formats**

### **a. Data Source Management Diagram**
- **Purpose**: Explain how `UITableViewController` handles different data sources and formats.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Static Data Sources**: Hardcoded data within the controller.
  - **Dynamic Data Sources**: Data fetched from APIs or databases.
  - **Core Data Integration**: Using `NSFetchedResultsController` for managing Core Data.
  - **JSON Parsing**: Handling JSON responses for dynamic content.
  - **Local Storage**: Integrating with `UserDefaults` or local databases.

```mermaid
graph LR
    A[UITableViewController Data Handling] --> B[Static Data Sources]
    A --> C[Dynamic Data Sources]
    A --> D[Core Data Integration]
    A --> E[JSON Parsing]
    A --> F[Local Storage]

    B --> B1[Hardcoded Data within Controller]

    C --> C1[Fetching Data from APIs]
    C --> C2[Loading Data from Databases]

    D --> D1[Using NSFetchedResultsController]
    D --> D2[Managing Core Data Entities]

    E --> E1[Handling JSON Responses]
    E --> E2[Parsing Data for Display]

    F --> F1[UserDefaults Integration]
    F --> F2[Local Database Access]
```

---

## **12. Integration with Drawing Contexts**

### **a. Table View Customization Diagram**
- **Purpose**: Show how `UITableViewController` methods are used to customize the appearance and behavior of table views.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Custom Cell Rendering**
  - **Header and Footer Customization**
  - **Row Animations**
  - **Accessory Views**
  - **Section Indexing**

## TODO: Fix diagram syntax error

```mermaid
flowchart TD
    UIImageController[UITableViewController] -->|Customizes| CustomCells[Custom Cell Rendering]
    UIImageController -->|Customizes| HeadersFooters[Header and Footer Customization]
    UIImageController -->|Handles| RowAnimations[Row Animations]
    UIImageController -->|Adds| AccessoryViews[Accessory Views]
    UIImageController -->|Manages| SectionIndexing[Section Indexing]

    CustomCells -->|Implement| tableView(_:cellForRowAt:)
    HeadersFooters -->|Implement| tableView(_:viewForHeaderInSection:)
    HeadersFooters -->|Implement| tableView(_:heightForHeaderInSection:)
    RowAnimations -->|Use| beginUpdates()/endUpdates()
    AccessoryViews -->|Configure| UITableViewCell.AccessoryType
    SectionIndexing -->|Implement| sectionIndexTitles(for:)
    
```

---

## **13. Summary and Best Practices**

### **a. Summary Diagram**
- **Purpose**: Provide a high-level overview of `UITableViewController`'s key characteristics and functionalities.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Efficient Data Management**
  - **Seamless User Interactions**
  - **Customization Flexibility**
  - **Integration Capabilities**
  - **Performance Optimizations**

```mermaid
graph LR
    A[UITableViewController] --> B[Efficient Data Management]
    A --> C[Seamless User Interactions]
    A --> D[Customization Flexibility]
    A --> E[Integration Capabilities]
    A --> F[Performance Optimizations]

    B --> B1[Managing Data Sources]
    B --> B2[Using Diffable Data Sources]

    C --> C1[Handling Selections and Actions]
    C --> C2[Implementing Context Menus]

    D --> D1[Custom Cell Designs]
    D --> D2[Flexible Layouts]

    E --> E1[Integrating with APIs and Databases]
    E --> E2[Using Storyboards and Nibs]

    F --> F1[Optimizing Row Heights]
    F --> F2[Efficient Memory Usage]
```

### **b. Best Practices Checklist Diagram**
- **Purpose**: Outline best practices when using `UITableViewController`.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Data Source Management**
  - **Cell Reuse Optimization**
  - **Efficient Layouts**
  - **Accessibility Compliance**
  - **Performance Monitoring**
  - **Smooth Animations**

```mermaid
flowchart LR
    A[Best Practices for UITableViewController] --> B[Data Source Management]
    A --> C[Cell Reuse Optimization]
    A --> D[Efficient Layouts]
    A --> E[Accessibility Compliance]
    A --> F[Performance Monitoring]
    A --> G[Smooth Animations]

    B --> B1[Use Diffable Data Sources]
    B --> B2[Handle Data Updates Gracefully]

    C --> C1[Dequeue Reusable Cells Efficiently]
    C --> C2[Configure Cells Properly]

    D --> D1[Implement Auto Layout Constraints]
    D --> D2[Use Self-Sizing Cells]

    E --> E1[Support VoiceOver]
    E --> E2[Ensure Proper Contrast and Sizing]

    F --> F1[Profile with Instruments]
    F --> F2[Minimize Memory Footprint]

    G --> G1[Implement Batch Updates]
    G --> G2[Use Core Animation Wisely]
```

---