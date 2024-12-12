---
created: 2024-12-07 04:58:55
url:
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
---


# UITableView

Below is a comprehensive and organized set of Mermaid diagrams for the `UITableView` framework. These diagrams cover various aspects of `UITableView`, including class hierarchy, initializers, properties, methods, enumerations, protocol conformances, relationships with other classes, extensions, lifecycle, feature availability, data handling, drawing contexts, and best practices.

---

## **1. Class Structure and Hierarchy**

### **a. Core Class Diagram**
- **Purpose**: Illustrate the primary structure of `UITableView`, including its properties, methods, and enumerations.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Properties**: Key attributes like `dataSource`, `delegate`, `rowHeight`, etc.
  - **Methods**: Essential functions like `reloadData()`, `register()`, `dequeueReusableCell()`, etc.
  - **Enumerations**: Nested enums such as `UITableView.Style`, `UITableView.RowAnimation`, etc.

```mermaid
classDiagram
    class UITableView {
        +dataSource: UITableViewDataSource?
        +delegate: UITableViewDelegate?
        +style: UITableView.Style
        +rowHeight: CGFloat
        +separatorStyle: UITableViewCell.SeparatorStyle
        +isEditing: Bool
        +reloadData()
        +register(UITableViewCell.Type, forCellReuseIdentifier: String)
        +dequeueReusableCell(withIdentifier: String) -> UITableViewCell?
        +insertRows(at: [IndexPath], with: UITableView.RowAnimation)
        +deleteRows(at: [IndexPath], with: UITableView.RowAnimation)
        // Additional properties and methods...
    }

    class Style {
        <<enum>>
        +plain
        +grouped
        +insetGrouped
        +sidebar
    }

    class RowAnimation {
        <<enum>>
        +fade
        +right
        +left
        +top
        +bottom
        +none
        +middle
        +automatic
    }

    UITableView --> Style
    UITableView --> RowAnimation
```

---

## **2. Initializers Overview**

### **a. Initialization Methods Diagram**
- **Purpose**: Break down the various ways to instantiate `UITableView`.
- **Diagram Type**: `flowchart` or `graph LR`
- **Contents**:
  - **Style-Based Initializers**: `init(frame:style:)`
  - **Storyboard & XIB**: Initialization via Interface Builder
  - **Programmatic Initialization**: Creating tables programmatically

```mermaid
graph LR
    A[UITableView Initializers] --> B[Style-Based Initializers]
    A --> C[Storyboard & XIB]
    A --> D[Programmatic Initialization]

    B --> B1["init(frame: CGRect, style: UITableView.Style)"]

    C --> C1["@IBDesignable UITableView"]

    D --> D1["init()"]
    D --> D2["required init?(coder: NSCoder)"]
```

---

## **3. Properties Breakdown**

### **a. Key Properties Diagram**
- **Purpose**: Detail the main properties of `UITableView`.
- **Diagram Type**: `graph LR` or `classDiagram`
- **Contents**:
  - **Data Management**: `dataSource`, `delegate`, `numberOfSections`
  - **Appearance**: `rowHeight`, `separatorStyle`, `backgroundView`
  - **Behavioral Attributes**: `isEditing`, `allowsSelection`, `allowsMultipleSelection`

```mermaid
graph LR
    A[UITableView Properties] --> B[Data Management]
    A --> C[Appearance]
    A --> D[Behavioral Attributes]

    B --> B1[dataSource: UITableViewDataSource?]
    B --> B2[delegate: UITableViewDelegate?]
    B --> B3[numberOfSections: Int]

    C --> C1[rowHeight: CGFloat]
    C --> C2[separatorStyle: UITableViewCell.SeparatorStyle]
    C --> C3[backgroundView: UIView?]

    D --> D1[isEditing: Bool]
    D --> D2[allowsSelection: Bool]
    D --> D3[allowsMultipleSelection: Bool]
```

---

## **4. Methods Grouped by Functionality**

### **a. Data Management Methods**
- **Purpose**: Categorize methods based on their roles in managing table data.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Reloading Data**: `reloadData()`
  - **Inserting and Deleting Rows/Sections**: `insertRows()`, `deleteRows()`, etc.
  - **Moving Rows**: `moveRow(at:to:)`
  - **Batch Updates**: `beginUpdates()`, `endUpdates()`

```mermaid
flowchart TD
    A[UITableView Methods] --> B[Reloading Data]
    A --> C[Inserting & Deleting Rows/Sections]
    A --> D[Moving Rows]
    A --> E[Batch Updates]

    B --> B1["reloadData()"]

    C --> C1["insertRows(at:with:)"]
    C --> C2["deleteRows(at:with:)"]
    C --> C3["insertSections(_:with:)"]
    C --> C4["deleteSections(_:with:)"]

    D --> D1["moveRow(at: IndexPath, to: IndexPath)"]

    E --> E1["beginUpdates()"]
    E --> E2["endUpdates()"]
```

### **b. Cell Management Methods**
- **Purpose**: Categorize methods related to cell creation and reuse.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Registering Cells**: `register(_:forCellReuseIdentifier:)`
  - **Dequeuing Cells**: `dequeueReusableCell(withIdentifier:for:)`
  - **Configuring Cells**: `cellForRow(at:)`

```mermaid
flowchart TD
    A[Cell Management Methods] --> B[Registering Cells]
    A --> C[Dequeuing Cells]
    A --> D[Configuring Cells]

    B --> B1["register(UITableViewCell.Type, forCellReuseIdentifier: String)"]
    C --> C1["dequeueReusableCell(withIdentifier: String, for: IndexPath) -> UITableViewCell"]
    D --> D1["cellForRow(at: IndexPath) -> UITableViewCell"]
```

### **c. Editing Methods**
- **Purpose**: Categorize methods that facilitate editing operations.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Begin/End Editing**: `setEditing(_:animated:)`
  - **Commit Editing**: `commit(_:forRowAt:)`

```mermaid
flowchart TD
    A[Editing Methods] --> B[Begin/End Editing]
    A --> C[Commit Editing]

    B --> B1["setEditing(Bool, animated: Bool)"]

    C --> C1["commit editingStyle: UITableViewCell.EditingStyle, forRowAt: IndexPath"]
```

---

## **5. Enumerations and Configurations**

### **a. Enumerations Diagram**
- **Purpose**: Highlight the enums used within `UITableView` and their possible values.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **UITableView.Style**
  - **UITableView.RowAnimation**
  - **UITableViewCell.SelectionStyle**
  - **UITableViewCell.SeparatorStyle**

```mermaid
classDiagram
    class UITableView {
        <<enumeration>> Style
        <<enumeration>> RowAnimation
    }

    class UITableViewCell {
        <<enumeration>> SelectionStyle
        <<enumeration>> SeparatorStyle
    }

    class Style {
        +plain
        +grouped
        +insetGrouped
        +sidebar
    }

    class RowAnimation {
        +fade
        +right
        +left
        +top
        +bottom
        +none
        +middle
        +automatic
    }

    class SelectionStyle {
        +none
        +blue
        +gray
        +default
    }

    class SeparatorStyle {
        +none
        +singleLine
        +singleLineEtched
    }

    UITableView --> Style
    UITableView --> RowAnimation
    UITableViewCell --> SelectionStyle
    UITableViewCell --> SeparatorStyle
```

### **b. Configuration Classes Diagram**
- **Purpose**: Show the relationship between `UITableView` and its configuration classes.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **UITableViewConfiguration**
  - **UITableViewRowAction** (Deprecated but relevant)
  - **UITableViewDragDelegate**
  - **UITableViewDropDelegate**

```mermaid
classDiagram
    class UITableView {
        +configuration: UITableViewConfiguration
        +dragDelegate: UITableViewDragDelegate?
        +dropDelegate: UITableViewDropDelegate?
    }

    class UITableViewConfiguration {
        // Configuration properties
    }

    class UITableViewDragDelegate {
        <<protocol>>
        // Drag delegate methods
    }

    class UITableViewDropDelegate {
        <<protocol>>
        // Drop delegate methods
    }

    UITableView --> UITableViewConfiguration
    UITableView --> UITableViewDragDelegate
    UITableView --> UITableViewDropDelegate
```

---

## **6. Protocol Conformances**

### **a. Protocols Diagram**
- **Purpose**: Display the protocols that `UITableView` conforms to and their impact.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **UIScrollViewDelegate**
  - **UITableViewDataSource**
  - **UITableViewDelegate**
  - **NSCoding**
  - **UIDataSourcePrefetching**

```mermaid
classDiagram
    class UITableView {
        <<open class>>
    }

    class UIScrollViewDelegate {
        <<protocol>>
    }

    class UITableViewDataSource {
        <<protocol>>
    }

    class UITableViewDelegate {
        <<protocol>>
    }

    class NSCoding {
        <<protocol>>
    }

    class UIDataSourcePrefetching {
        <<protocol>>
    }

    UITableView ..|> UIScrollViewDelegate
    UITableView ..|> UITableViewDataSource
    UITableView ..|> UITableViewDelegate
    UITableView ..|> NSCoding
    UITableView ..|> UIDataSourcePrefetching
```

---

## **7. Relationships with Other Classes**

### **a. Related Classes Diagram**
- **Purpose**: Illustrate how `UITableView` interacts with other UIKit classes and frameworks.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **UITableViewCell**: Represents individual cells.
  - **UITableViewHeaderFooterView**: Represents header and footer views.
  - **UIScrollView**: As a superclass.
  - **UIRefreshControl**: For pull-to-refresh functionality.
  - **UITableViewController**: Controller managing the table view.
  - **NSIndexPath**: Identifies sections and rows.
  - **UITableViewDiffableDataSource**: Modern data source management.
  - **UITableViewRowAction**: For swipe actions (deprecated in favor of UIContextualAction).

```mermaid
flowchart TD
    A[UITableView] --> B[UITableViewCell]
    A --> C[UITableViewHeaderFooterView]
    A --> D[UIScrollView]
    A --> E[UIRefreshControl]
    A --> F[UITableViewController]
    A --> G[NSIndexPath]
    A --> H[UITableViewDiffableDataSource]
    A --> I[UITableViewRowAction]

    B --> |Represents| A
    C --> |Used for| A
    D --> |Superclass| A
    E --> |Enhances| A
    F --> |Manages| A
    G --> |Identifies rows| A
    H --> |Manages data| A
    I --> |Swipe actions| A
```

---

## **8. Extensions and Additional Functionalities**

### **a. UITableView Extensions Diagram**
- **Purpose**: Showcase the additional functionalities provided through extensions.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Convenience Methods**
  - **Registration Helpers**
  - **Batch Updates Enhancements**

```mermaid
classDiagram
    class UITableView {
        <<open class>>
    }

    class UITableViewExtensions {
        <<extension>>
        +func reloadData(completion: (() -> Void)?)
        +func register<T: UITableViewCell>(_: T.Type)
        +func dequeueReusableCell<T: UITableViewCell>(withIdentifier: String, for indexPath: IndexPath) -> T
        +func performBatchUpdates(_ updates: () -> Void, completion: ((Bool) -> Void)?)
        // Additional extended methods
    }

    UITableView <-- UITableViewExtensions
```

### **b. Extensions Functionalities Flowchart**
- **Purpose**: Detail specific extended methods and their purposes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Reload with Completion**
  - **Generic Cell Registration**
  - **Generic Cell Dequeuing**
  - **Enhanced Batch Updates**

```mermaid
flowchart LR
    A[UITableView Extensions] --> B[Reload with Completion]
    A --> C[Generic Cell Registration]
    A --> D[Generic Cell Dequeuing]
    A --> E[Enhanced Batch Updates]

    B --> B1["reloadData(completion: (() -> Void)?)"]

    C --> C1["register<T: UITableViewCell>(_: T.Type)"]

    D --> D1["dequeueReusableCell<T: UITableViewCell>(withIdentifier: String, for indexPath: IndexPath) -> T"]

    E --> E1["performBatchUpdates(_ updates: () -> Void, completion: ((Bool) -> Void)?)"]
```

---

## **9. Lifecycle and Use Cases**

### **a. Lifecycle Flowchart**
- **Purpose**: Demonstrate the typical lifecycle of a `UITableView` within an application.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Initialization**
  - **Registration of Cells**
  - **Data Loading**
  - **User Interaction**
  - **Updating Data**
  - **Reloading and Refreshing**
  - **Deallocation**

```mermaid
flowchart TD
    Start[Start] --> Init[Initialize UITableView]
    Init --> Register[Register Cells & Views]
    Register --> LoadData[Load Data via DataSource]
    LoadData --> Display[Display Cells]
    Display --> Interaction[Handle User Interaction]
    Interaction --> Update[Update Data]
    Update --> Reload[Reload or Update TableView]
    Reload --> Display
    Display --> Deallocation[Deallocate UITableView]
    Deallocation --> End[End]
```

### **b. Common Use Cases Diagram**
- **Purpose**: Outline the typical scenarios where `UITableView` is utilized.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Displaying Lists**
  - **Form Inputs**
  - **Settings Screens**
  - **Nested Tables**
  - **Dynamic Content Loading**
  - **Swipe Actions**
  - **Drag and Drop**

```mermaid
flowchart TD
    A[UITableView Use Cases] --> B[Displaying Lists]
    A --> C[Form Inputs]
    A --> D[Settings Screens]
    A --> E[Nested Tables]
    A --> F[Dynamic Content Loading]
    A --> G[Swipe Actions]
    A --> H[Drag and Drop]

    B --> B1["Contacts List"]
    B --> B2["Messages"]
    C --> C1["User Preferences"]
    D --> D1["App Settings"]
    E --> E1["Category with Sub-items"]
    F --> F1["Infinite Scrolling"]
    G --> G1["Delete, Edit Actions"]
    H --> H1["Reordering Cells"]
```

---

## **10. Feature Availability Timeline**

### **a. Feature Availability Gantt Chart**
- **Purpose**: Show when various `UITableView` features were introduced across iOS versions.
- **Diagram Type**: `gantt`
- **Contents**:
  - **iOS Versions**: 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 10.0, 11.0, 13.0, 14.0, 15.0, 16.0, 17.0
  - **Features Introduced**: Automatic Dimension, Swipe Actions, Drag and Drop, Diffable Data Sources, Self-Sizing Cells, etc.

## TODO: Fix diagram syntax error

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title UITableView Feature Availability

    section iOS 2.0
    Basic UITableView           :done, des1, 2008-07-11, 2008-07-11

    section iOS 3.0
    Editing Mode                :done, des2, 2009-06-17, 2009-06-17

    section iOS 4.0
    Section Indexing            :done, des3, 2010-06-21, 2010-06-21

    section iOS 5.0
    Automatic Row Animation     :done, des4, 2011-10-12, 2011-10-12

    section iOS 6.0
    Automatic Cell Height        :done, des5, 2012-09-19, 2012-09-19

    section iOS 7.0
    Swipe Actions                :done, des6, 2013-09-18, 2013-09-18

    section iOS 8.0
    Self-Sizing Cells            :done, des7, 2014-09-22, 2014-09-22

    section iOS 10.0
    Drag and Drop                :done, des8, 2016-09-19, 2016-09-19

    section iOS 11.0
    Drag & Drop Enhancements     :done, des9, 2017-09-19, 2017-09-19

    section iOS 13.0
    Diffable Data Sources        :done, des10, 2019-09-19, 2019-09-19

    section iOS 14.0
    UICollectionView Integration :done, des11, 2020-09-16, 2020-09-16

    section iOS 15.0
    UITableViewRowAction Deprecated :done, des12, 2021-09-20, 2021-09-20

    section iOS 16.0
    Collapsible Sections         :done, des13, 2022-09-12, 2022-09-12

    section iOS 17.0
    Enhanced Swipe Actions       :done, des14, 2023-09-18, 2023-09-18
    
```

---

## **11. Data Handling and Formats**

### **a. Data Source Protocol Diagram**
- **Purpose**: Explain how `UITableView` handles different data sources.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **UITableViewDataSource**
  - **UITableViewDiffableDataSource**
  - **UIDataSourcePrefetching**

```mermaid
flowchart LR
    A[UITableView] --> B[UITableViewDataSource]
    A --> C[UITableViewDiffableDataSource]
    A --> D[UIDataSourcePrefetching]

    B --> B1["numberOfSections(in:) -> Int"]
    B --> B2["tableView(_:numberOfRowsInSection:) -> Int"]
    B --> B3["tableView(_:cellForRowAt:) -> UITableViewCell"]

    C --> C4["snapshot() -> NSDiffableDataSourceSnapshot"]
    C --> C5["apply(_:animatingDifferences:)"]

    D --> D6["tableView(_:prefetchRowsAt:)"]
    D --> D7["tableView(_:cancelPrefetchingForRowsAt:)"]
```

### **b. Data Handling Diagram**
- **Purpose**: Detail how `UITableView` manages data and interacts with data sources.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Data Source Methods**
  - **Diffable Data Source**
  - **Prefetching Data**
  - **Snapshot Management**

```mermaid
flowchart TD
    A[Data Handling in UITableView] --> B[Data Source Methods]
    A --> C[Diffable Data Source]
    A --> D[Prefetching Data]
    A --> E[Snapshot Management]

    B --> B1["numberOfSections"]
    B --> B2["numberOfRowsInSection"]
    B --> B3["cellForRowAt"]

    C --> C4["Create Initial Snapshot"]
    C --> C5["Apply Snapshot with Animations"]

    D --> D6["tableView(_:prefetchRowsAt:)"]
    D --> D7["tableView(_:cancelPrefetchingForRowsAt:)"]

    E --> E8["NSDiffableDataSourceSnapshot"]
    E --> E9["Reapply Snapshot on Data Change"]
```

---

## **12. Integration with Drawing Contexts**

### **a. Custom Drawing in Cells Diagram**
- **Purpose**: Show how `UITableView` integrates with custom drawing contexts within cells.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Custom UITableViewCell**
  - **Drawing with Core Graphics**
  - **Animating Drawings**
  - **Performance Considerations**

```mermaid
flowchart TD
    A[Custom Drawing in Cells] --> B[Custom UITableViewCell]
    A --> C[Drawing with Core Graphics]
    A --> D[Animating Drawings]
    A --> E[Performance Considerations]

    B --> B1["Subclass UITableViewCell"]
    B --> B2["Override draw(_ rect: CGRect)"]

    C --> C1["Use CGContext for Custom Shapes"]
    C --> C2["Render Custom Graphics"]

    D --> D1["Animate Layer Properties"]
    D --> D2["Use UIView Animations"]

    E --> E3["Optimize Drawing Code"]
    E --> E4["Use Caching for Static Content"]
```

### **b. Highlighting and Selection Diagram**
- **Purpose**: Detail how drawing contexts are used for cell highlighting and selection.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Selection States**
  - **Highlighted State Drawing**
  - **Accessory Views Customization**

```mermaid
flowchart LR
    A[Highlighting & Selection] --> B[Selection States]
    A --> C[Highlighted State Drawing]
    A --> D[Accessory Views Customization]

    B --> B1["selected: Bool"]
    B --> B2["highlighted: Bool"]

    C --> C3["Override setSelected(_:animated:)"]
    C --> C4["Customize Appearance on Selection"]

    D --> D5["Custom Accessory Views"]
    D --> D6["Accessory Type Modification"]
```

---

## **13. Summary and Best Practices**

### **a. Summary Diagram**
- **Purpose**: Provide a high-level overview of `UITableView`'s key characteristics and functionalities.
- **Diagram Type**: `graph LR` or `mindmap`
- **Contents**:
  - **Versatile Data Management**
  - **Customizable Appearance**
  - **Efficient Cell Reuse**
  - **Enhanced User Interaction**
  - **Performance Optimizations**
  - **Modern Data Sources**

```mermaid
graph LR
    A[UITableView] --> B[Versatile Data Management]
    A --> C[Customizable Appearance]
    A --> D[Efficient Cell Reuse]
    A --> E[Enhanced User Interaction]
    A --> F[Performance Optimizations]
    A --> G[Modern Data Sources]

    B --> B1[DataSource & Delegate]
    B --> B2[Sections & Rows Management]

    C --> C3[Custom Cells]
    C --> C4[Headers & Footers]
    C --> C5[Styling & Theming]

    D --> D1[Reuse Identifiers]
    D --> D2[Cell Queuing Mechanism]

    E --> E3[Selection & Highlighting]
    E --> E4[Swipe Actions]
    E --> E5[Drag and Drop]

    F --> F6[Batch Updates]
    F --> F7[Prefetching Data]

    G --> G8[Diffable Data Sources]
    G --> G9[Combine Integration]
```

### **b. Best Practices Diagram**
- **Purpose**: Outline best practices for using `UITableView` effectively.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Reuse Identifiers Properly**
  - **Optimize Data Loading**
  - **Implement Prefetching**
  - **Use Diffable Data Sources**
  - **Customize Cells Efficiently**
  - **Handle Dynamic Heights**
  - **Ensure Smooth Scrolling**

```mermaid
flowchart LR
    A[Best Practices for UITableView] --> B[Reuse Identifiers Properly]
    A --> C[Optimize Data Loading]
    A --> D[Implement Prefetching]
    A --> E[Use Diffable Data Sources]
    A --> F[Customize Cells Efficiently]
    A --> G[Handle Dynamic Heights]
    A --> H[Ensure Smooth Scrolling]

    B --> B1["Register Cells Once"]
    B --> B2["Dequeue Reusable Cells"]

    C --> C3["Lazy Loading of Data"]
    C --> C4["Asynchronous Data Fetching"]

    D --> D5["Implement UIDataSourcePrefetching"]
    D --> D6["Cancel Unnecessary Prefetches"]

    E --> E7["Adopt NSDiffableDataSourceSnapshot"]
    E --> E8["Simplify Data Updates"]

    F --> F9["Use Lightweight Cell Configurations"]
    F --> F10["Avoid Heavy Operations in Cell"]

    G --> G11["Use Automatic Dimension"]
    G --> G12["Ensure Proper Constraints"]

    H --> H13["Optimize Cell Layout"]
    H --> H14["Minimize Overdraw"]
```

---
