---
created: 2025-03-28 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Text & Font System - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


Showing `Text` view capabilities and the `Font` struct.

```mermaid
---
title: "SwiftUI Framework - Text & Font System"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  layout: elk
  look: handDrawn
  theme: dark
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%%%%%%% Toggle theme value to `base` to activate the initilization below for the customized theme version.
%%%%%%%% Available curve styles include the following keywords:
%% basis, bumpX, bumpY, cardinal, catmullRom, linear, monotoneX, monotoneY, natural, step, stepAfter, stepBefore.
%%{
  init: {
    'graph': { 'htmlLabels': false, 'curve': 'linear' },
    'fontFamily': 'Fantasy',
    'themeVariables': {
      'primaryColor': '#ffff',
      'primaryTextColor': '#55ff',
      'primaryBorderColor': '#7c2',
      'lineColor': '#F8B229',
      'secondaryColor': '#006100',
      'tertiaryColor': '#fff'
    }
  }
}%%
graph TD
    subgraph TextView["Text View"]
        T_Text(Text) -- Initializers --> T_Inits["String, LocalizedStringKey, AttributedString, Formatter, FormatStyle, Date, Image, ..."]
        T_Text -- Modifiers --> T_Mods["foregroundColor(), font(), fontWeight(), italic(), strikethrough(), underline(), kerning(), tracking(), baselineOffset(), textCase(), monospacedDigit(), ..."]
        T_Text -- Layout Modifiers --> T_LayoutMods["lineLimit(), multilineTextAlignment(), truncationMode(), allowsTightening(), minimumScaleFactor(), lineSpacing(), ..."]
        T_Text -- Localization --> LocalizedStringKey
        TextLayout(Text.Layout) -- Lines --> TextLine(Text.Layout.Line)
        TextLine -- Runs --> TextRun(Text.Layout.Run)
        TextRun -- Slices --> TextRunSlice(Text.Layout.RunSlice)
        T_Text -- Query Layout --> TextLayout
    end

    subgraph FontStruct["Font Struct"]
        F_Font(Font) -- System Fonts --> F_System[".largeTitle, .title, .body, .caption, ..."]
        F_Font -- System Initializers --> F_SysInit[".system(size:weight:design:), .system(style:design:weight:)"]
        F_Font -- Custom Initializers --> F_CustomInit[".custom(name:size:), .custom(name:fixedSize:), Font(CTFont)"]
        F_Font -- Modifiers --> F_Mods[".italic(), .smallCaps(), .monospacedDigit(), .weight(), .bold(), .monospaced(), .leading(), .width()"]
        F_Font -- Nested Types --> F_Nested["Font.TextStyle, Font.Design, Font.Weight, Font.Width, Font.Leading"]
    end

    subgraph TextAttributes["Text Styling"]
        TA_AttributedString(AttributedString) -- Used by --> T_Text
        TA_Markdown["Markdown Support"] -- Parsed into --> TA_AttributedString
        
        %% TA_LineStyle(Text.LineStyle) -- Used for --> T_Mods -- "underline/strikethrough"
        TA_LineStyle(Text.LineStyle) -- Used for --> T_Mods 
        T_Mods -- "underline/strikethrough" --> TA_LineStyle
        
        TA_LinePattern(Text.LineStyle.Pattern) -- ".solid, .dot, .dash, ..." --> TA_LineStyle

        %% TA_TextCase(Text.Case) -- ".uppercase, .lowercase" --> T_Mods -- "textCase()"
        TA_TextCase(Text.Case) -- ".uppercase, .lowercase" --> T_Mods 
        TA_TextCase -- "textCase()" --> T_Mods 

        %% TA_TextScale(Text.Scale) -- ".default, .secondary" --> T_Mods -- "textScale()"
        TA_TextScale(Text.Scale) -- ".default, .secondary" --> T_Mods
        TA_TextScale -- "textScale()" --> T_Mods

        %% TA_TypesettingLanguage(TypesettingLanguage) -- ".automatic, .explicit()" --> T_Mods -- "typesettingLanguage()"
        TA_TypesettingLanguage(TypesettingLanguage) -- ".automatic, .explicit()" --> T_Mods
        TA_TypesettingLanguage -- "typesettingLanguage()" --> T_Mods
        
        %% TA_TextAttribute(TextAttribute Protocol) -- Applied via --> T_Mods -- ".customAttribute()"
        TA_TextAttribute(TextAttribute Protocol) -- Applied via --> T_Mods
        TA_TextAttribute -- ".customAttribute()" --> T_Mods
    end

    T_Text -- ".font()" --> F_Font
    
```

----


**Explanation:** This diagram details the `Text` view, its initializers, and modifiers for styling and layout. It also shows the `Font` struct, how to create system or custom fonts, and available font modifiers and nested types (TextStyle, Design, Weight, etc.). Associated types like `Text.LineStyle` and `Text.Case` are included.



---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---